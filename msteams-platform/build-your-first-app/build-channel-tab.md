---
title: Начало работы — создание вкладки канала и группы
author: girliemac
description: Быстро создайте канал Microsoft Teams и вкладку группы с помощью microsoft Teams набор средств.
ms.author: timura
ms.date: 03/22/2020
ms.topic: tutorial
ms.openlocfilehash: 868a471499bf2015196b7b741e340d070d0ed458
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068754"
---
# <a name="build-your-first-channel-and-group-tab-for-microsoft-teams"></a>Создание вкладки первого канала и группы для Microsoft Teams

В этом руководстве рассказывается  о создании базовой вкладки канала, также известной как вкладка *группы,* которая является полноэкранной страницей для канала или чата группы. Вы также можете настроить некоторые аспекты вкладки такого типа, например, переименовать вкладку, чтобы она была значимой для канала, что невозможно сделать в личной вкладке.

## <a name="what-youll-learn"></a>Что вы узнаете

* Создайте проект приложения с помощью microsoft Teams набор средств для Visual Studio Code.
* Разберем конфигурации приложений и леса, соответствующие вкладке канала.
* Создание конфигурации контента и вкладок.
* Создайте и запустите приложение в командах для тестирования.

## <a name="prerequisites"></a>Необходимые условия

Убедитесь, что вы понимаете, как настроить и создать простое приложение Teams. Дополнительные сведения см. в [вашем первом приложении Microsoft Teams "Hello, World!".](../build-your-first-app/build-and-run.md)

## <a name="1-create-your-app-project"></a>1. Создание проекта приложения

Программа Microsoft Teams набор средств настроить приложение и настроить леса, соответствующие вкладке канала и группы. В нем также содержится базовая страница конфигурации и страница контента, на которую отображается "Hello, World!". Сообщение.

**Создание проекта приложения**

1. Перейдите Visual Studio код и выберите **Microsoft Teams** в левой :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: панели действий.
1. Во входе в учетную запись разработки Microsoft 365 при запросе на это.
1. На экране **Выберите проект** выберите **JS** (JavaScript) в **приложении Channel и group.**
1. Введите имя приложения Teams. 

    > [!NOTE]
    > Это имя по умолчанию для вашего приложения, а также имя каталога проектов приложений на локальной машине.

1. Выберите **вкладку канала Group или Teams.**
1. Выберите **Готово** в нижней части экрана, чтобы настроить проект и сохранить проект на локальной машине.  

## <a name="2-understand-your-app-project-components"></a>2. Понимание компонентов проекта приложения

Большая часть конфигураций приложений и строительных лесов создается автоматически при создании проекта с помощью набора инструментов. Рассмотрим основные компоненты для создания вкладки канала.

* **Конфигурации приложений:** Откройте **App Studio** в наборе инструментов для просмотра и обновления конфигураций приложений.
* **Строительные леса** приложений. Строительные леса приложений предоставляют компоненты, необходимые для отрисовки вкладки канала в Teams. Тем не менее, вы можете много работать, но теперь давайте сосредоточимся на следующем:
  * Файлы, расположенные в `src/components` каталоге проекта:
    * `Tab.js` для отрисовки страницы контента вкладки.
    * `TabConfig.js` для отрисовки страницы конфигурации вкладки.
  * Клиент Microsoft Teams JavaScript SDK, который поставляется с предварительной загрузкой в передние компоненты проекта.

## <a name="3-customize-your-tab-content-page"></a>3. Настройка страницы контента вкладок

1. Скопируйте и измените следующий пример кода с помощью сведений, соответствующих организации. Фрагмент можно также использовать так, как это:
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
1. Перейдите в `src/components` каталог и откройте `Tab.js` файл. Найдите `render()` функцию и вклейте код `return()` внутри, как показано в следующем примере:
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
1. Перейдите в каталог и обнови файл следующим кодом, чтобы упростить чтение ссылок электронной почты в любой `src/components` `App.css` используемой теме:
    ```CSS
    a {
      color: inherit;
    }
    ```

## <a name="4-customize-your-tab-configuration-page"></a>4. Настройка страницы конфигурации вкладок

Каждая вкладка в канале или чате имеет страницу конфигурации, модал с по крайней мере одним параметром настройки, отображаемой при добавлении приложения пользователями. Страница конфигурации по умолчанию спрашивает пользователей, хотят ли они уведомить канал или чат при установке вкладки. Вы можете настроить страницу конфигурации, добавив настраиваемый контент.

Чтобы добавить настраиваемый контент, откройте файл из каталога и обновив содержимое держателя внутри, как показано `TabConfig.js` `src/components` в следующем `return()` примере:

  ```JavaScript
  return (
      <div>
        <h1>Add My Contoso Contacts</h1>
        <div>
          Select <b>Save</b> to add our organization's important contacts to this workspace.
        </div>
      </div>
  );
  ```
 
> [!TIP]
> Дайте краткую информацию о вашем приложении на этой странице, так как это будет первый раз, когда пользователи читают об этом. Вы также можете включить настраиваемые параметры конфигурации или рабочий процесс проверки [подлинности,](../tabs/how-to/authentication/auth-aad-sso.md)который распространен на страницах конфигурации вкладок.

## <a name="5-customize-your-tab-name"></a>5. Настройка имени вкладки

При добавлении вкладки канала имя приложения отображает по умолчанию, например, **первое приложение.** Вы также можете предоставить имя, которое имеет больше смысла в контексте групповой совместной работы, например, **Team Contacts:**

1. Перейдите в `src/components` каталог и откройте `TabConfig.js` файл.
1. Добавьте свойство с именем вкладки, которое необходимо отобразить по умолчанию, как `suggestedDisplayName` `microsoftTeams.settings.setSettings` показано в следующем примере:

  ```JavaScript
    microsoftTeams.settings.setSettings({
    "contentUrl": "https://localhost:3000/tab",
    "suggestedDisplayName": "Team Contacts"
  });
  ```

## <a name="6-build-and-run-your-app"></a>6. Сборка и запуск приложения

Этот учебник учит создавать и запускать приложение локально. 

1. Перейдите в корневой каталог проекта приложения в Терминале.
1. Запуск `npm install` .
1. Запуск `npm start` .

Эти сведения также представлены в `README` разделе набор инструментов.
Ваше приложение работает после `https://localhost:3000` **успешного компилировать!** сообщение отображается в терминале. 

## <a name="7-sideload-your-app-in-teams"></a>7. Боковое загрузка приложения в Teams

Ваше приложение готово для тестирования в Teams. Для этого необходимо иметь учетную запись, позволяющую загрузку приложений. 

1. Откройте веб-клиент Teams в Visual Studio коде с **ключом F5.**
1. Добавление () в качестве надежного, следуя этим шагам, чтобы включить отображение контента приложения `localhost` в Teams:

   1. Откройте новую вкладку в том же окне браузера (Google Chrome по умолчанию), которая открылась с помощью **клавиши F5.**
   1. Откройте `https://localhost:3000/tab` и переехав на страницу.

1. Выберите **Добавить в команду или** **добавить** в чат и найти канал или чат, который можно использовать для тестирования из модуля в Teams.
1. Выберите **Настройка вкладки**. Страница конфигурации отображается в модале.

   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="Снимок экрана страницы конфигурации вкладок канала.":::

1. Выберите **Сохранить,** чтобы настроить вкладку. Появится следующая страница контента:

   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="Снимок экрана вкладки канала со статическим представлением контента.":::

## <a name="see-also"></a>См. также

* [Создание и запуск первого приложения Microsoft Teams](../build-your-first-app/build-and-run.md) 
* [Клиентский SDK JavaScript для Teams](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* [Разработка вкладки для настольных и веб-страниц Microsoft Teams](../tabs/design/tabs.md) 
* [Разработка приложения Microsoft Teams с помощью шаблонов пользовательского интерфейса](../concepts/design/design-teams-app-ui-templates.md) 
* [Вкладки на мобильных устройствах](../tabs/design/tabs-mobile.md)
* [Поддержка единого входного знака (SSO) для вкладок](../tabs/how-to/authentication/auth-aad-sso.md)
* [Обзор API Microsoft Teams](https://docs.microsoft.com/graph/teams-concept-overview)
* [Создание настраиваемой личной вкладки с Node.js и генератором Yeoman для Microsoft Teams](../tabs/quickstarts/create-personal-tab-node-yeoman.md)

## <a name="next-step"></a>Следующий шаг

> [!div class="nextstepaction"]
> [Создание бота](../build-your-first-app/build-bot.md)

> [!div class="nextstepaction"]
> [Создание расширения для сообщений](../build-your-first-app/build-messaging-extension.md)