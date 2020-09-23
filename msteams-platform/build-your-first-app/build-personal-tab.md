---
title: Создание вкладки группы "Личное"
author: heath-hamilton
description: Узнайте, как создать личную вкладку для первого приложения Microsoft Teams.
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: tutorial
ms.openlocfilehash: 3b54efa9b7ed8019b5d4901eeaaf0864e1afc7ac
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/22/2020
ms.locfileid: "48210219"
---
# <a name="build-a-teams-personal-tab"></a>Создание вкладки группы "Личное"

Вкладки — это простой способ отображения контента в приложении, по сути внедряя веб-страницу в Teams.

В Teams есть два типа вкладок. В этом руководстве вы создадите базовую *вкладку личное*, страницу содержимого на полном экране для отдельных пользователей. (Личные вкладки — это ближайшее к традиционному интерфейсу веб-сайта в Teams.)

## <a name="before-you-begin"></a>Прежде чем начать

Для начала необходимо создать базовую вкладку выполнение личных настроек. Если у вас его нет, ознакомьтесь [со статьей Создание и запуск первого приложения Teams](../build-your-first-app/build-and-run.md).

## <a name="your-assignment"></a>Ваше назначение

Сотрудникам Организации не удается найти основные контактные данные для важных функций (служба технической поддержки, HR и т. д.). Вы следите за тем, чтобы они могли быстро найти эту информацию в одном месте. Как это сделать? Разумеется, личная вкладка группы Teams.

## <a name="what-youll-learn"></a>Что вы узнаете

> [!div class="checklist"]
>
> * Определение некоторых свойств манифеста приложения и формирование шаблонов, относящихся к личным вкладкам
> * Создание содержимого вкладки
> * Обновление темы цвета вкладки в соответствии с предпочтениями пользователя

## <a name="identify-relevant-app-project-components"></a>Определение соответствующих компонентов проекта приложения

Большинство манифестов и шаблонов приложений настраиваются автоматически при создании проекта с помощью набора инструментов Teams. Рассмотрим основные компоненты для создания вкладки личных сведений.

### <a name="app-manifest"></a>Манифест приложения

Показан следующий фрагмент манифеста приложения ( `manifest.json` файл в `.publish` каталоге проекта) [`staticTabs`](../resources/schema/manifest-schema.md#statictabs) , который включает свойства и значения по умолчанию, относящиеся к личным вкладкам.

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

* `entityId`: Уникальный идентификатор страницы, отображаемой на вкладке.
* `name`: Отображаемое имя вкладки (например, "My Contacts").
* `contentUrl`: URL-адрес узла страница содержимого вкладки (должна быть HTTPS).
* `scopes`: Указывает, что вкладка предназначена только для личного пользования.

### <a name="app-scaffolding"></a>Формирование шаблонов приложений

Формирование шаблонов приложений предоставляет компоненты для отображения вкладки в Teams. Существует множество способов, с которыми вы можете работать, но теперь вам нужно сосредоточиться на следующих задачах:

* `Tab.js` файл в `src/components` каталоге проекта
* Клиентский пакет SDK Microsoft Teams JavaScript, который предварительно загружен в интерфейсных компонентах проекта.

## <a name="create-your-tab-content"></a>Создание содержимого вкладки

Скомпилируйте список важных контактов в Организации. Скопируйте и обновите следующий фрагмент кода со сведениями, важными для вас или, в целях простоты, используйте код как есть.

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

Перейдите в `src/components` каталог и откройте его `Tab.js` . Нахождение `render()` функции и вставка содержимого внутри `return()` (как показано на рисунке).

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

Добавьте следующее правило, чтобы `App.css` ссылки электронной почты легче читались независимо от того, какая тема используется.

```CSS
a {
  color: inherit;
}
```

Сохраните изменения. Перейдите на вкладку приложения в Teams, чтобы просмотреть новый контент.

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-content.png" alt-text="Снимок экрана: личная вкладка со статическим содержимым.":::

## <a name="update-the-tab-theme"></a>Обновление темы вкладки

Хорошие приложения в Teams встроены в Teams, поэтому для вкладок важна тема, в которую пользователи предпочитают: по умолчанию (Light), темный или High контрастность. Как вы могли заметить на последнем снимке экрана, вкладка по-прежнему имеет светлый фон, когда клиент использует темную тему. Это не рекомендуемый пользовательский интерфейс.

[Пакет SDK для Teams JavaScript](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) может сделать ваше приложение осведомленным об изменениях темы в клиенте и реагировать на них. Давайте разберем, как это сделать.

### <a name="get-context-about-the-teams-client"></a>Получение контекста о клиенте Teams

В `Tab.js` файле существует `microsoftTeams.getContext()` вызов, который предоставляет некоторые сведения [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) о настроенной клиентской теме (помимо других сведений). Благодаря формированию шаблонов приложений используйте этот код, чтобы получить доступ к `context` интерфейсу и его свойствам.

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

### <a name="create-a-theme-change-handler"></a>Создание обработчика изменений темы

Если у `context` вас есть свойства в наличии, ваше приложение имеет твердое представление о происходящих в Teams. Но приложение по-прежнему не знает, что его внешний вид должен отражать любую тему, которую выбрал пользователь.

Необходимо обработчик, чтобы изменить состояние приложения с помощью темы. Вставьте следующий обработчик изменений темы сразу после `microsoftTeams.getContext()` вызова.

```JavaScript
  microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.theme) {
      this.setState({ theme });  
    }
  });
```

### <a name="match-theme-styles"></a>Сравнение стилей темы

Ваш обработчик изменений темы размещается, но вам необходим код, который реагирует на эти изменения и выравнивает цвета вкладки с помощью текущей темы.

> [!NOTE]
> Приведенный ниже пример можно использовать только один из способов применения стилей к вкладке. Используйте код как есть, разверните его или напишите собственное.

Сохраните состояние, предоставленное обработчиком изменений темы, в файле `isTheme` .

```JavaScript
  const isTheme = this.state.theme
```

Предоставляет некоторую условную логику для отображения стилей вкладок на основе текущей темы. В следующем примере показан простой способ, выполняемый на 1) при проверке текущей темы в `isTheme` , 2) создание `newTheme` объекта со свойствами CSS, относящимися к текущей теме, и 3) применение CSS к корневому элементу HTML содержимого вкладки ( `<div>` ).

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

Проверьте вкладку в Teams. Внешний вид должен точно соответствовать темной теме.

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-updated-theme.png" alt-text="Снимок экрана со вкладкой "Личное" и представлением статического содержимого.":::

## <a name="well-done"></a>Прекрасно

Поздравляем! У вас есть приложение Teams со вкладкой "личные", которая упрощает поиск важных контактов в Организации.

## <a name="learn-more"></a>Подробнее

* [Проверка подлинности пользователей вкладки с единым входом](../tabs/how-to/authentication/auth-aad-sso.md): Если вы хотите, чтобы авторизованные пользователи просматривали вкладку, настройте единый вход (SSO) через Azure Active Directory (AD).
* [Внедрение контента из существующего веб-приложения или веб-страницы](../tabs/how-to/add-tab.md#tab-requirements): мы показали, как создать новое содержимое для вкладки личных данных, но вы также можете загрузить контент с внешнего URL-адреса.
* [Создайте простой интерфейс для вкладки](../tabs/design/tabs.md): Ознакомьтесь с рекомендациями по проектированию вкладок Teams.
* [Создание вкладок для мобильных устройств](../tabs/design/tabs-mobile.md): Узнайте, как создавать вкладки для телефонов и планшетов.
* [Интеграция с API Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview)
* [Создание вкладки без набора инструментов](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a>Следующий урок

Вы знаете, как создать вкладку для личного использования. Рассмотрим, что требуется для создания вкладки для каналов команд и чатов.

> [!div class="nextstepaction"]
> [Создание вкладки канала](../build-your-first-app/build-channel-tab.md)
