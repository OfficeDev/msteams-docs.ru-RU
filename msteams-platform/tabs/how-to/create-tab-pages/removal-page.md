---
title: Создать страницу удаления вкладки
author: surbhigupta
description: Создание страницы удаления вкладок
keywords: группы вкладок группового канала, настраиваемые удалить удаление
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 97f5dfdd8cd9e5e19ec26c345ac960a04a108ab3
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179715"
---
# <a name="create-a-removal-page"></a>Создать страницу удаления

Вы можете расширить и улучшить пользовательский интерфейс, поддержав параметры удаления и изменения в приложении. Teams позволяет пользователям переименовать или удалить вкладку канала или группы, и вы можете разрешить пользователям перенастройку вкладки после установки. Кроме того, функции удаления вкладок предоставляют пользователям возможность удаления или удаления контента.

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a>Включить перенастройку вкладки после установки

Ваша **manifest.jsопределяет** функции и возможности вкладки. Свойство экземпляра вкладки принимает значение Boolean, которое указывает, может ли пользователь изменить или перенастроить вкладку после `canUpdateConfiguration` ее создания. В следующей таблице приводится информация о свойстве:

|Имя| Тип| Максимальный размер | Обязательный | Описание|
|---|---|---|---|---|
|`canUpdateConfiguration`|Логический|||Значение, указывающее, может ли экземпляр конфигурации вкладки обновляться пользователем после создания. Значение по умолчанию: `true`. |

Когда вкладка загружается в канал или групповой чат, Teams добавляет для вкладки выпадаемое меню правой кнопкой мыши. Доступные параметры определяются `canUpdateConfiguration` параметром. В следующей таблице ниже параметров параметров:

| `canUpdateConfiguration`| true   | false | description |
| ----------------------- | :----: | ----- | ----------- |
|     Параметры            |   √    |       |Страница `configurationUrl` перезагружается в IFrame, что позволяет пользователю перенастроить вкладку. |
|     Переименовать              |   √    |   √   | Пользователь может изменить имя вкладки, как оно отображается в панели вкладок.          |
|     Удалить              |   √    |   √   |  Если свойство и значение включены в страницу конфигурации, страница удаления загружается в `removeURL` IFrame и представляется пользователю.   Если страница удаления не включена, пользователю будет представлен диалоговое окно с подтверждением.          |

## <a name="create-a-tab-removal-page-for-your-application"></a>Создание страницы удаления вкладок для приложения

Необязательная страница удаления — это htmL-страница, на которую вы выводили и отображали при удалении вкладки. URL-адрес страницы удаления назначается методом `setSettings()` на странице конфигурации. Как и все страницы в приложении, страница удаления должна соответствовать требованиям Teams [вкладки.](../../../tabs/how-to/tab-requirements.md)

### <a name="register-a-remove-handler"></a>Регистрация обработера удаления

Необязательно, в логике удаления страницы можно вызвать обработтель событий, когда пользователь удаляет `registerOnRemoveHandler((RemoveEvent) => {}` существующую конфигурацию вкладки. Метод принимает интерфейс и выполняет код в обработнике, когда пользователь [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest&preserve-view=true) пытается удалить контент. Метод используется для выполнения операций очистки, таких как удаление основному ресурсу, вещаемому контентом вкладки. Одновременно можно зарегистрировать только один обработник удаления.

Интерфейс `RemoveEvent` описывает объект двумя методами:

* Функция `notifySuccess()` необходима. Это указывает на успешное удаление этого ресурса, а его содержимое можно удалить.

* Функция `notifyFailure(string)` необязательна. Это указывает на то, что удаление основному ресурсу не удалось и его содержимое невозможно удалить. Необязательный параметр строки указывает причину сбоя. При условии эта строка отображается пользователю; кроме того, отображается общая ошибка.

#### <a name="use-the-getsettings-function"></a>Использование `getSettings()` функции

Вы можете `getSettings()` назначить удаляемому содержимому вкладки. Функция принимает и предоставляет допустимые значения свойств `getSettings((Settings) =>{})` [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) параметров, которые можно получить.

#### <a name="use-the-getcontext-function"></a>Использование `getContext()` функции

Вы можете использовать `getContext()` для получения текущего контекста, в котором работает кадр. Функция `getContext((Context) =>{})` принимает в [`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) . Функция предоставляет допустимые значения свойств, которые можно использовать в логике страницы удаления, чтобы определить содержимое, отображаемую `Context` на странице удаления.

#### <a name="include-authentication"></a>Включить проверку подлинности

Проверка подлинности требуется, прежде чем разрешить пользователю удалять содержимое вкладки. Сведения о контексте можно использовать для создания запросов на проверку подлинности и URL-адресов страниц авторизации. См. [Microsoft Teams поток проверки подлинности для вкладок.](~/tabs/how-to/authentication/auth-flow-tab.md) Убедитесь, что все домены, используемые на страницах вкладок, перечислены в `manifest.json` `validDomains` массиве.

Ниже приводится пример блока кода удаления вкладок:

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

Когда пользователь выбирает **Удаление** из выпадаемого меню вкладки, Teams загружает необязательные страницы, заданная на странице конфигурации, в `removeUrl` IFrame.  Пользователю показана кнопка, загруженная функцией, которая вызывает и включает кнопку Удалить, показанную в нижней части страницы `onClick()` `microsoftTeams.settings.setValidityState(true)` удаления IFrame. 

После выполнения обработка удаления или Teams `removeEvent.notifySuccess()` `removeEvent.notifyFailure()` результатов удаления контента.

>[!NOTE]
> * Чтобы не препятствовать контролю авторизованного пользователя над вкладками, Teams удаляет вкладку как в случаях успешного, так и неудачного.
> * Teams кнопку **Удалить** через пять секунд, даже если вкладка не вызвала `setValidityState()` .
> * Когда пользователь выбирает **Remove,** Teams удаляет вкладку через 30 секунд независимо от того, завершены действия или нет.

## <a name="see-also"></a>См. также

* [Teams вкладки](~/tabs/what-are-tabs.md)
* [Создание личной вкладки](~/tabs/how-to/create-personal-tab.md)
* [Создание вкладки канала или группы](~/tabs/how-to/create-channel-group-tab.md)
* [Создать страницу конфигурации](~/tabs/how-to/create-tab-pages/configuration-page.md)

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Вкладки на мобильных устройствах](~/tabs/design/tabs-mobile.md)