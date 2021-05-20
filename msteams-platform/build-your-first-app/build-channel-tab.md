---
title: Начало работы - Создание канала и вкладки группы
author: girliemac
description: Быстро создайте Microsoft Teams канал и групповую вкладку с помощью Microsoft Teams набор средств.
ms.author: timura
ms.date: 03/22/2020
ms.topic: tutorial
ms.openlocfilehash: ff9cfbfb7d099db52966f119add4ce8729929aa1
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566070"
---
# <a name="build-your-first-channel-and-group-tab-for-microsoft-teams"></a>Создайте свой первый канал и групповую вкладку для Microsoft Teams

Этот учебник научит вас строить основные вкладки *канала также* известный как группа *вкладка*, которая является полноэкранной страницей для командного канала или чата. Вы также можете настроить некоторые аспекты такого рода вкладок, например, переименовать вкладку, чтобы она была значимой для их канала, что вы не можете сделать в личной вкладке.

## <a name="what-youll-learn"></a>Чему вы научитесь

* Создайте проект приложения, используя Microsoft Teams набор средств для Visual Studio Code.
* Поймите конфигурации приложений и леса, относящиеся к вкладок канала.
* Создание содержимого вкладок и конфигурации вкладок.
* Создавайте и запускайте приложение в командах для тестирования.

## <a name="prerequisites"></a>Предварительные требования

Убедитесь, что вы понимаете, как настроить и построить простой Teams приложение. Для получения дополнительной [информации, см Microsoft Teams.](../build-your-first-app/build-and-run.md)

## <a name="1-create-your-app-project"></a>1. Создание проекта приложения

Проект Microsoft Teams набор средств вам настроить приложение и настроить леса, имеющие отношение к вкладок канала и группы. Он также содержит основную страницу конфигурации и содержание страницы, которая отображает "Здравствуйте, мир!" Сообщение.

**Создание проекта приложения**

1. Перейдите Visual Studio Code и **выберите Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: на левой стойке активности.
1. Вопишитесь в свой аккаунт Microsoft 365 разработки, когда вам будет предложено это сделать.
1. На **экране проекта Select** выберите **JS** (JavaScript) под **приложением Channel и group.**
1. Введите имя для вашего Teams приложения. 

    > [!NOTE]
    > Это имя по умолчанию для вашего приложения, а также название каталога проекта приложения на локальной машине.

1. Выберите **вкладку Teams канала.**
1. **Выберите** отделку в нижней части экрана, чтобы настроить проект и сохранить проект на локальной машине.  

## <a name="2-understand-your-app-project-components"></a>2. Понимание компонентов проекта приложения

Большая часть конфигураций приложений и строительных лесов настроены автоматически при создании проекта с помощью инструментария. Рассмотрим основные компоненты для построения вкладки канала.

* **Конфигурации приложений**: Open **App Studio** в наборе инструментов для просмотра и обновления конфигураций приложений.
* **App леса :** приложение леса предоставляет компоненты, необходимые для рендеринга вашего канала вкладку в Teams. Там очень много вы можете работать, однако, на данный момент давайте сосредоточимся на следующем:
  * Файлы, на которые `src/components` находится каталог вашего проекта:
    * `Tab.js` для рендеринга страницы содержимого вкладки.
    * `TabConfig.js` для визуализации страницы конфигурации вкладки.
  * Microsoft Teams JavaScript клиент SDK, который поставляется предварительно загружены в передней части компонентов вашего проекта.

## <a name="3-customize-your-tab-content-page"></a>3. Настройка страницы содержимого вкладок

1. Копировать и изменять следующий образец кода с информацией, относящейся к вашей организации. Вы также можете использовать фрагмент, как он есть:
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
    
1. Зайдите в `src/components` каталог и откройте `Tab.js` файл. Найдите `render()` функцию и вставьте код `return()` внутрь, как показано в следующем примере:
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
    
1. Перейдите в `src/components` каталог и обновите файл со следующим кодом, чтобы сделать `App.css` ссылки электронной почты легче читать в любой теме, которая используется:
    ```CSS
    a {
      color: inherit;
    }
    ```

## <a name="4-customize-your-tab-configuration-page"></a>4. Настройка страницы конфигурации вкладок

Каждая вкладка в канале или чате имеет страницу конфигурации, модал с по крайней мере одним вариантом настройки, который отображается при использовании приложения пользователями. Страница конфигурации по умолчанию запрашивает пользователей, хотят ли они уведомить канал или чат при установке вкладки. Вы можете настроить страницу конфигурации, добавив пользовательский контент.

Чтобы добавить пользовательский контент, откройте `TabConfig.js` файл из `src/components` каталога и обновив содержимое заполнителя `return()` внутри, как показано в следующем примере:

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
> Дайте краткую информацию о вашем приложении на этой странице, так как это будет первый раз, когда пользователи читают об этом. Вы также можете включить пользовательские параметры конфигурации или рабочий [процесс проверки подлинности,](../tabs/how-to/authentication/auth-aad-sso.md)который является общим на страницах конфигурации вкладок.

## <a name="5-customize-your-tab-name"></a>5. Настроили имя вкладки

При добавление вкладки канала имя приложения отображается по умолчанию, например, **первым приложением.** Вы также можете узнать имя, которое имеет больше смысла в контексте совместной работы группы, например, **Контакты группы:**

1. Зайдите в `src/components` каталог и откройте `TabConfig.js` файл.
1. Добавьте `suggestedDisplayName` свойство с именем вкладки, которое вы хотите отобразить по умолчанию, `microsoftTeams.settings.setSettings` как показано в следующем примере:

    ```JavaScript
        microsoftTeams.settings.setSettings({
        "contentUrl": "https://localhost:3000/tab",
        "suggestedDisplayName": "Team Contacts"
      });
      ```

## <a name="6-build-and-run-your-app"></a>6. Создание и запуск приложения

Этот учебник научит вас создавать и запускать приложение локально. 

1. Перейдите в корневой каталог проекта приложения в Терминале.
1. Запуск `npm install` .
1. Запуск `npm start` .

Эта информация также представлена `README` в разделе инструментария.
Ваше приложение работает после `https://localhost:3000` **успешного составления!** сообщение отображается в терминале. 

## <a name="7-sideload-your-app-in-teams"></a>7. Sideload ваше приложение в Teams

Ваше приложение готово к тестированию в Teams. Для этого необходимо иметь учетную запись, которая позволяет перезагрузить приложение. 

1. Откройте Teams веб-клиента Visual Studio Code с помощью **ключа F5.**
1. Добавить `localhost` () в качестве надежного, следуя этим шагам, чтобы содержимое приложения отображаться в Teams:

   1. Откройте новую вкладку в том же окне браузера (Google Chrome по умолчанию), которая открылась с **ключом F5.**
   1. Откройте `https://localhost:3000/tab` и перейти к странице.

1. Выберите **Добавить в команду** или Добавить в чат **и** найти канал или чат можно использовать для тестирования от модала в Teams.
1. Выберите **настройку вкладки**. Страница конфигурации отображается в моде.

   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="Скриншот страницы конфигурации вкладки канала.":::

1. Выберите **Сохранить** для настройки вкладки. Отображается следующая страница содержимого:

   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="Скриншот вкладки канала со статическим представлением содержимого.":::

## <a name="see-also"></a>См. также

* [Создание и запуск первого Microsoft Teams приложения](../build-your-first-app/build-and-run.md) 
* [Клиентский SDK JavaScript для Teams](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* [Проектирование вкладки для Microsoft Teams и веб-страниц](../tabs/design/tabs.md) 
* [Проектирование приложения Microsoft Teams с помощью шаблонов пользовательского интерфейса](../concepts/design/design-teams-app-ui-templates.md) 
* [Вкладки на мобильных устройствах](../tabs/design/tabs-mobile.md)
* [Поддержка вкладок с одним ва-пом (SSO)](../tabs/how-to/authentication/auth-aad-sso.md)
* [Обзор API Microsoft Teams](/graph/teams-concept-overview)
* [Создайте пользовательскую личную вкладку с Node.js и генератором Yeoman для Microsoft Teams](../tabs/quickstarts/create-personal-tab-node-yeoman.md)

## <a name="next-step"></a>Следующий шаг

> [!div class="nextstepaction"]
> [Создание бота](../build-your-first-app/build-bot.md)

> [!div class="nextstepaction"]
> [Создание расширения для сообщений](../build-your-first-app/build-messaging-extension.md)
