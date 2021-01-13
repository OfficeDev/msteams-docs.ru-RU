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
# <a name="build-a-personal-tab-for-microsoft-teams"></a>Создание личной вкладки для Microsoft Teams

Вкладки — это простой способ выставлять содержимое в приложении, встраив веб-страницу в Teams.

В Teams существует два типа вкладок. В этом руководстве вы создайте базовую *личную* вкладку — полноэкранную страницу содержимого для отдельных пользователей. (Личные вкладки — это самое близкое к традиционному веб-сайту в Teams.)

## <a name="before-you-begin"></a>Прежде чем начать

Для начала вам потребуется базовая запущенная личная вкладка. Если у вас его нет, см. сборку и [запустите свое первое приложение Teams.](../build-your-first-app/build-and-run.md)

## <a name="your-assignment"></a>Назначение

У людей в организации проблемы с поиском основных контактных данных для важных функций (службы поддержки, отдела кадров и т. д.). Вы отвечаете за то, чтобы они могли быстро найти эти сведения в одном месте. Как это сделать? Конечно, личная вкладка Teams.

## <a name="what-youll-learn"></a>Что вы узнаете

> [!div class="checklist"]
>
> * Определение некоторых конфигураций приложений и скаолдинг, релевантный для личных вкладок
> * Создание содержимого вкладок
> * Обновление цветовой темы вкладки в зависимости от предпочтений пользователя

## <a name="1-identify-relevant-app-project-components"></a>1. Определение соответствующих компонентов проекта приложения

Большая часть конфигураций и скафаолдинга приложений автоматически заданная при создании проекта с помощью командной набор средств. Рассмотрим основные компоненты для создания личной вкладки.

### <a name="app-configurations"></a>Конфигурации приложений

В наборе инструментов перейдите в **App Studio,** чтобы просмотреть и обновить конфигурации приложений.

### <a name="app-scaffolding"></a>Скафаолдинг приложений

Скафолдинг приложения предоставляет компоненты для отображения личной вкладки в Teams. Вы можете работать с большим количеством работы, но на данный момент вам нужно сосредоточиться только на следующих темах:

* `Tab.js` файл в `src/components` каталоге проекта. Это для отображения страницы содержимого вкладки.
* Клиентский SDK JavaScript для Microsoft Teams, который предварительно загружается в клиентские компоненты вашего проекта.

## <a name="2-customize-your-tab-content-page"></a>2. Настройка страницы содержимого вкладки

Скомпилировать список важных контактов в организации. Скопируйте и обновим следующий фрагмент с информацией, которая вам актуальна, или используйте код как есть.

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

Перейдите в `src/components` каталог и откройте `Tab.js` . Найдите `render()` функцию и в paste содержимое `return()` внутри (как показано).

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

Добавьте следующее правило, чтобы упростить чтение ссылок электронной почты независимо от `App.css` используемой темы.

```CSS
a {
  color: inherit;
}
```

Сохраните изменения. Перейдите на вкладку приложения в Teams, чтобы просмотреть новое содержимое.

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-content.png" alt-text="Снимок экрана: личная вкладка со статическим содержимым.":::

## <a name="3-update-the-tab-theme"></a>3. Обновление темы вкладки

Хорошие приложения, которые отлично работают с Teams, поэтому важно, чтобы ваша вкладка смешивала тему Teams, предпочитаемую вашими пользователями: по умолчанию (светлая), темная или высокая контрастность. Как вы могли заметить на последнем снимке экрана, при использовании клиентом темной темы на вкладке по-прежнему остается светлый фон. Это не рекомендуется для пользователей.

Клиентский [SDK JavaScript](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) для Teams позволяет вашему приложению реагировать на изменения тем в клиенте. Рассмотрим, как это сделать.

### <a name="get-context-about-the-teams-client"></a>Получите контекст о клиенте Teams

В файле есть вызов, который предоставляет некоторые сведения о настроенной теме `Tab.js` `microsoftTeams.getContext()` [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) клиента. Благодаря скафаолдингу приложения используйте этот код так же, как и для доступа к интерфейсу `context` и его свойствам.

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

### <a name="create-a-theme-change-handler"></a>Создание обработера изменений темы

Благодаря свойствам в приложении вы четко понимаете, что происходит с ним `context` в Teams. Но приложение по-прежнему не знает, что его внешний вид должен отражать любую тему, выбираемую пользователем.

Вам нужен обработок, чтобы состояние приложения менялось с темой. Вставьте следующий обработок изменения темы сразу после `microsoftTeams.getContext()` вызова.

```JavaScript
  microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.theme) {
      this.setState({ theme });  
    }
  });
```

### <a name="match-theme-styles"></a>Соответствие стилям темы

Обработник изменений темы уже существует, но вам нужен код, который реагирует на эти изменения и выравнивает цвета вкладки с текущей темой.

> [!NOTE]
> В следующем примере вы можете применять стили только к вкладке. Используйте код как есть, развяйте его или напишите свое.

В `render()` функции сберегать состояние, предоставленное обработом изменения темы, в `isTheme` .

```JavaScript
  const isTheme = this.state.theme
```

После с хранения состояния, предоставленного обработом изменения темы, предоберите условную логику для отрисовки стилей вкладки на основе текущей темы. В следующем примере показан базовый способ сделать это:
1. Проверьте текущую тему в `isTheme` .
2. Создайте `newTheme` объект со свойствами CSS, соответствующими текущей теме.
3. Примените CSS к корневому HTML-элементу содержимого вкладки ( `<div>` ).

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

Проверьте вкладку в Teams. Внешний вид должен близко соответствовать темной теме.

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-updated-theme.png" alt-text="Снимок экрана: личная вкладка со статическим представлением содержимого.":::

## <a name="well-done"></a>Прекрасно

Поздравляем! У вас есть приложение Teams с личной вкладками, которая упрощает поиск важных контактов в вашей организации.

## <a name="learn-more"></a>Подробнее

* [Проверка подлинности](../tabs/how-to/authentication/auth-aad-sso.md)пользователей вкладок с помощью единого входного набора: если вы хотите, чтобы на вкладке просматривали только авторизованные пользователи, необходимо настроить единый вход с помощью Azure Active Directory (AD).
* [Встраивайте](../tabs/how-to/tab-requirements.md)содержимое из существующего веб-приложения или веб-страницы: мы показали вам, как создать новое содержимое для личной вкладки, но вы также можете загрузить содержимое с внешнего URL-адреса.
* [Органично создайте вкладку:](../tabs/design/tabs.md)см. рекомендации по проектированию вкладок Teams.
* [Создание вкладок для мобильных устройств.](../tabs/design/tabs-mobile.md)В этой теме вы знаете, как разрабатывать вкладки для телефонов и планшетов.
* [Использование данных Teams с Помощью Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview)
* [Создание вкладки без наборов средств](../tabs/quickstarts/create-channel-group-tab-node-yeoman.md)

## <a name="next-lesson"></a>Следующий урок

Вы знаете, как создать вкладку для личного использования. Рассмотрим, что требуется для создания вкладки для каналов и чатов команды.

> [!div class="nextstepaction"]
> [Создание вкладки канала](../build-your-first-app/build-channel-tab.md)
