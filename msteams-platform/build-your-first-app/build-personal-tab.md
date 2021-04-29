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
# <a name="build-a-basic-personal-tab-for-microsoft-teams"></a>Создание базовой личной вкладки для Microsoft Teams

В этом руководстве рассказывается о создании базовой личной вкладки в Microsoft Teams. Вкладки — это простой способ получения сведений в приложении путем размещения веб-контента в Teams. Вкладки — это общая функция личных приложений, которые предоставляют личное рабочее пространство для отдельных пользователей. Личные вкладки ближе всего к традиционному веб-опыту в Teams. 

## <a name="what-youll-learn"></a>Что вы узнаете

* Понимание конфигураций приложений и строительных лесов, соответствующих личным вкладкам.
* Создание контента вкладки со списком контактов организации.
* Обновление цветовой темы вкладки с учетом предпочтений пользователей.

## <a name="prerequisites"></a>Необходимые условия

Убедитесь, что вы понимаете, как настроить и создать простое приложение Teams. Дополнительные сведения см. в [вашем первом приложении Microsoft Teams "Hello, World!".](../build-your-first-app/build-and-run.md)

## <a name="1-understand-your-app-project-components"></a>1. Понимание компонентов проекта приложения

После создания базовой личной вкладки созданный эшафот приложения предоставляет компоненты для отрисовки личной вкладки в Teams. Вы можете много работать, но сейчас давайте сосредоточимся на следующем: 

* `Tab.js` файл в `src/components` каталоге проекта. Это для отрисовки страницы контента вкладок.
* Клиент Microsoft Teams JavaScript SDK, предварительно загруженный в компоненты переднего компонента проекта.

Как вы можете заметить из раздела в верхней части файла, пример кода использует React — библиотеку JavaScript с открытым исходным кодом для создания `import` `Tabs.js` пользовательского интерфейса. [](https://reactjs.org/) 

> [!NOTE]
> Хотя использование React _не требуется_ для разработки Teams, этот учебник учит вас с React.

## <a name="2-customize-your-tab-content-page"></a>2. Настройка страницы контента вкладок

Вы можете настроить страницу контента вкладок для отображения списка важных контактов в организации. 

**Настройка страницы контента вкладок**

1. Скопируйте и измените следующий пример кода с помощью соответствующих сведений. Код также можно использовать так: 
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
1. Добрался до `src/components` каталога и открыл `Tab.js` файл. 
1. Перейдите `render()` и замените код шаблона измененным кодом `return()` внутри, как показано в следующем примере:
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
1. Перейдите в каталог и измените файл со следующим кодом, чтобы облегчить чтение ссылок электронной почты с помощью любой `src/components` `App.css` используемой темы:
    ```CSS
    a {
      color: inherit;
    }
    ```
1. Сохраните изменения. 

   Новое содержимое можно просмотреть на вкладке приложения в Teams.

   :::image type="content" source="../assets/images/build-your-first-app/personal-tab-tutorial-content.png" alt-text="Снимок экрана личной вкладки со статическим контентом.":::

## <a name="3-update-your-tab-theme"></a>3. Обновление темы вкладки

Важно, чтобы в вкладке была тема, которая является родным для Teams. Вкладку необходимо смешать с темой Teams. Обычно пользователи предпочитают темы по умолчанию (светлые), темные или высококонтрентные. Как вы могли заметить на последнем скриншоте, вкладка по-прежнему имеет светлый фон, когда пользователь использует темную тему. Это не рекомендуется для пользователей.

SDK клиента Teams JavaScript может сделать ваше приложение осведомленным об изменениях темы в клиенте и реагировать на них. Для этого выполните следующие действия:

1. **Получите контекст для настраиваемой клиентской темы Teams** Вызов в файле содержит определенный контекст настроенной клиентской темы `microsoftTeams.getContext()` `Tab.js` (например, темная тема). Следующий код имеет доступ к `context` интерфейсу и его свойствам:

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
1. **Создание обработера изменения темы** С свойствами в руках, ваше приложение имеет четкое представление о том, что происходит `context` вокруг него в Teams. Однако при обновлении пользователя у приложения по-прежнему нет внешнего вида, отражающий тему.

   Чтобы обновить состояние приложения с помощью темы, необходим обработок. Чтобы создать обработник, вставьте следующий обработник изменения темы сразу после `microsoftTeams.getContext()` вызова:

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
1. **Соответствие стилям темы** Однако обработник изменения темы должен реагировать на изменения и выравнивать цвета вкладки с текущей темой.

   В этой `render()` функции храните состояние, предоставленное обработить изменение темы `isTheme` в:

    ```JavaScript
      const isTheme = this.state.context.theme
    ```
    
    > [!NOTE]
    > В этом примере можно применить стили к вкладке. Используйте код как есть, расширите его или напишите свой собственный.

    После хранения состояния, предоставленного обработив изменение темы, указайте условную логику для отображения стилей вкладки на основе текущей темы. В следующем примере показан базовый способ сделать это:

    1. Перейдите `render()` и проверьте текущую тему в `isTheme` .
    1. Создайте `newTheme` объект со свойствами CSS, соответствующими текущей теме.
    1. Применить следующий CSS к корневому элементу HTML контента вкладки `<div style={newTheme}>` ():

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

       Проверьте вкладку в Teams. Внешний вид теперь тесно совпадает с темной темой.

       :::image type="content" source="../assets/images/build-your-first-app/personal-tab-tutorial-updated-theme.png" alt-text="Снимок экрана личной вкладки со статическим представлением контента.":::

## <a name="see-also"></a>См. также

* [Клиентский SDK JavaScript для Teams](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* [Разработка вкладки для настольных и веб-страниц Microsoft Teams](../tabs/design/tabs.md) 
* [Интерфейс контекста](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true)
* [Разработка приложения Microsoft Teams с помощью шаблонов пользовательского интерфейса](../concepts/design/design-teams-app-ui-templates.md) 
* [Вкладки на мобильных устройствах](../tabs/design/tabs-mobile.md)
* [Поддержка единого входного знака (SSO) для вкладок](../tabs/how-to/authentication/auth-aad-sso.md)
* [Обзор API Microsoft Teams](https://docs.microsoft.com/graph/teams-concept-overview)
* [Создание настраиваемой личной вкладки с Node.js и генератором Yeoman для Microsoft Teams](../tabs/quickstarts/create-personal-tab-node-yeoman.md)

## <a name="next-step"></a>Следующий шаг

> [!div class="nextstepaction"]
> [Создание вкладки канала](../build-your-first-app/build-channel-tab.md)