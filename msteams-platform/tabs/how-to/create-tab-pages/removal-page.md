---
title: Создать страницу удаления вкладки
author: surbhigupta
description: Узнайте, как включить перенастройку вкладки после установки. Расширение пользовательского интерфейса за счет поддержки параметров удаления и изменения в приложении Microsoft Teams.
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 6aa06cae222ad89b89b2eddc0ba224db0ff4225f
ms.sourcegitcommit: 87bba925d005eb331d876a0b9b75154f8100e911
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2022
ms.locfileid: "67450410"
---
# <a name="create-a-removal-page"></a>Создать страницу удаления

Вы можете расширить и улучшить взаимодействие с пользователем, поддерживая параметры удаления и изменения в своем приложении. Teams позволяет пользователям переименовывать или удалять вкладку канала или группы, и вы можете разрешить пользователям изменять конфигурацию вкладки после установки. Кроме того, функция удаления вкладки предоставляет пользователям возможность после удаления удалить или заархивировать содержимое.

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a>Включить перенастройку вкладки после установки

`manifest.json` определяет функции и возможности вкладки. Свойство экземпляра табуляции `canUpdateConfiguration` принимает логическое значение, указывающее, может ли пользователь изменить или перенастроить вкладку после ее создания. В следующей таблице приведены сведения о свойстве:

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`canUpdateConfiguration`|Логический|||Значение, указывающее, может ли экземпляр конфигурации вкладки быть обновлен пользователем после создания. Значение по умолчанию — `true` |

Когда вкладка загружается в канал или групповой чат, Teams добавляет раскрывающееся меню правой кнопкой мыши для вкладки. Доступные параметры определяются параметром `canUpdateConfiguration`. В следующей таблице приведены сведения о настройках:

| `canUpdateConfiguration`| true   | false | description |
| ----------------------- | :----: | ----- | ----------- |
|     Settings            |   √    |       |Страница `configurationUrl` перезагружается в IFrame, что позволяет пользователю перенастроить вкладку. |
|     Переименовать              |   √    |   √   | Пользователь может изменить отображение имени вкладки на панели вкладок.          |
|     Удалить              |   √    |   √   |  Если свойство `removeURL` и значение включены в **страницу конфигурации**, **страница удаления** загружается в IFrame и представляется пользователю. Если страница удаления не включена, пользователю предоставляется диалоговое окно подтверждения.          |

## <a name="create-a-tab-removal-page-for-your-application"></a>Создайте страницу удаления вкладки для своего приложения

Необязательная страница удаления — это HTML-страница, которая отображается при удалении вкладки. URL-адрес страницы удаления `setConfig()` назначается методом ( `setSettings()` или до TeamsJS версии 2.0.0) на странице конфигурации. Как и все страницы в приложении, страница удаления должна соответствовать [предварительным требованиям вкладки Teams](../../../tabs/how-to/tab-requirements.md).

### <a name="register-a-remove-handler"></a>Зарегистрировать обработчик удаления

При необходимости в логике страницы `registerOnRemoveHandler((RemoveEvent) => {}` удаления можно вызвать обработчик событий, когда пользователь удаляет существующую конфигурацию вкладки. Метод принимает интерфейс [`RemoveEvent`](/javascript/api/@microsoft/teams-js/pages.config.removeevent?view=msteams-client-js-latest&preserve-view=true) и выполняет код в обработчике, когда пользователь пытается удалить содержимое. Этот метод используется для выполнения операций очистки, таких как удаление базового ресурса, питающего содержимое вкладки. Одновременно может быть зарегистрирован только один обработчик удаления.

Интерфейс `RemoveEvent` описывает объект двумя способами:

* Функция`notifySuccess()` обязательна. Это указывает на то, что удаление базового ресурса прошло успешно и его содержимое может быть удалено.

* Функция `notifyFailure(string)` необязательна. Это означает, что удаление базового ресурса завершилось сбоем и его содержимое невозможно удалить. Необязательный параметр строки указывает причину сбоя. Если эта строка задана, она отображается для пользователя; иначе отображается общая ошибка.

#### <a name="use-the-getconfig-function"></a>Использование функции `getConfig()`

Вы можете использовать `getConfig()` (ранее `getSettings()`) для назначения удаляемого содержимого вкладки. Функция `getConfig()` возвращает обещание, которое разрешается с объектом Config и предоставляет допустимые значения свойств параметров, которые можно получить.

#### <a name="use-the-getcontext-function"></a>Использование функции `getContext()`

Вы можете использовать `getContext()` для получения текущего контекста, в котором запущен фрейм. Функция `getContext()` возвращает обещание, которое будет разрешаться с помощью объекта Context. Объект Context предоставляет допустимые `Context` значения свойств, которые можно использовать в логике страницы удаления для определения содержимого, отображаемого на странице удаления.

#### <a name="include-authentication"></a>Включить проверку подлинности

Перед тем, как разрешить пользователю удалять содержимое вкладки, требуется проверка подлинности. Контекстные сведения можно использовать для создания запросов аутентификации и URL-адресов страниц авторизации. См. [Поток проверки подлинности Microsoft Teams для вкладок](~/tabs/how-to/authentication/auth-flow-tab.md) Убедитесь, что все домены, используемые на страницах вкладок, `validDomains` перечислены в массиве манифеста приложения.

Ниже приведен образец блока кода удаления вкладки:

# <a name="teamsjs-v2"></a>[TeamsJS версии 2](#tab/teamsjs-v2)

```html
<body>
  <button onclick="onClick()">Delete this tab and all underlying data?</button>
  <script type="module">
        import {app, pages} from 'https://res.cdn.office.net/teams-js/2.0.0/js/MicrosoftTeams.min.js';
    await app.initialize();
    pages.config.registerOnRemoveHandler((removeEvent) => {
      // Here you can designate the tab content to be removed and/or archived.
        const configPromise = pages.getConfig();
        configPromise.
            then((configuration) => {
                configuration.contentUrl = "...";
                removeEvent.notifySuccess()}).
            catch((error) => {removeEvent.notifyFailure("failure message")});
    });

    const onClick() => {
        pages.config.setValidityState(true);
    }
  </script>
</body>
```

# <a name="teamsjs-v1"></a>[TeamsJS версии 1](#tab/teamsjs-v1)

```html
<body>
  <button onclick="onClick()">Delete this tab and all underlying data?</button>
  <script>
    microsoftTeams.initialize();
    microsoftTeams.settings.registerOnRemoveHandler((removeEvent) => {
      // Here you can designate the tab content to be removed and/or archived.
        microsoftTeams.settings.getSettings((settings) => {
        settings.contentUrl = "..."
        });
        removeEvent.notifySuccess();
    });

    const onClick() => {
        microsoftTeams.settings.setValidityState(true);
    }
  </script>
</body>
```

***

Когда пользователь выбирает **Удалить** из меню вкладки, Teams загружает дополнительную страницу `removeUrl`, назначенную в **настройках страницы**, в IFrame. Пользователю показывается кнопка с функцией `onClick()`, вызова `pages.config.setValidityState(true)` и активации кнопки **Удалить**, показанной в нижней части страницы удаления IFrame.

После действия обработчика удаления`removeEvent.notifySuccess()` или `removeEvent.notifyFailure()` уведомления Teams о результатах удаления содержимого.

>[!NOTE]
>
> * Чтобы гарантировать, что контроль авторизованного пользователя над вкладкой не запрещен, Teams удаляет вкладку как в случае успеха, так и в случае сбоя.
> * После вызова обработчика событий `registerOnRemoveHandler` у вас будет 15 секунд, чтобы отреагировать на метод. По умолчанию Teams включает кнопку **Удалить** через пять секунд, даже если вы не вызываете `setValidityState(true)`.
> * Когда пользователь выбирает **Удалить**, Teams удаляет вкладку через 30 секунд независимо от того, завершены ли действия.

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Вкладки на мобильных устройствах](~/tabs/design/tabs-mobile.md)

## <a name="see-also"></a>Дополнительные ресурсы

* [Вкладки Teams](~/tabs/what-are-tabs.md)
* [Создание личной вкладки](~/tabs/how-to/create-personal-tab.md)
* [Создание вкладки канала или группы](~/tabs/how-to/create-channel-group-tab.md)
* [Создать страницу конфигурации](~/tabs/how-to/create-tab-pages/configuration-page.md)
