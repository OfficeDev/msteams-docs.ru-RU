---
title: Создать страницу контента
author: surbhigupta
description: Сведения о веб-странице в клиенте Teams, которая является частью личной, каналной или групповой настраиваемой вкладки. Создайте страницу содержимого и внедрите ее в виде веб-представления внутри модуля задач.
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 34e106bfa0fdfa6b881d1a2fcd5685c022ac5d87
ms.sourcegitcommit: 87bba925d005eb331d876a0b9b75154f8100e911
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2022
ms.locfileid: "67450375"
---
# <a name="create-a-content-page"></a>Создать страницу контента

Страница содержимого — это веб-страница, отображаемая в клиенте Teams, которая является частью:

* Настраиваемая вкладка с личной областью действия: в этом случае страница содержимого — это первая страница, с которой сталкивается пользователь.
* Настраиваемая вкладка канала или группы: страница содержимого отображается после того, как пользователь закрепит и настроит вкладку в соответствующем контексте.
* [Модуль задач](~/task-modules-and-cards/what-are-task-modules.md): вы можете создать страницу содержимого и встроить ее как веб-представление в модуль задач. Страница отображается внутри модального всплывающего окна.

Эта статья относится к использованию страниц содержимого в качестве вкладок. Однако большинство рекомендаций здесь применимо независимо от того, как страница содержимого представлена пользователю.

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="tab-content-and-design-guidelines"></a>Содержимое вкладок и рекомендации по дизайну

Общая цель вкладки — предоставить доступ к содержательному и привлекательному содержимому, которое имеет практическое значение и явную цель.

Вам нужно сосредоточиться на том, чтобы сделать макет вкладки понятным, интуитивно понятным и иммерсивным содержимым. Дополнительные сведения см. в [руководствах по проектированию вкладок](~/tabs/design/tabs.md) и рекомендациях по проверке [магазина Microsoft Teams](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md).

## <a name="integrate-your-code-with-teams"></a>Интегрируйте свой код с Teams

Чтобы страница отображалась в Teams, нужно включить [клиентский SDK Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) для JavaScript и включить вызов `app.initialize()` после загрузки страницы.

> [!NOTE]
> Изменение содержимого или пользовательского интерфейса для отражения в приложении вкладки из-за кэша занимает около 24–48 часов.

В следующем коде показан пример взаимодействия вашей страницы и клиента Teams.

# <a name="teamsjs-v2"></a>[TeamsJS версии 2](#tab/teamsjs-v2)

```html
<!DOCTYPE html>
<html>
<head>
...
    <script src= 'https://res.cdn.office.net/teams-js/2.0.0/js/MicrosoftTeams.min.js'></script>
...
<body>
...
    <script type="module">
        import {app} from 'https://res.cdn.office.net/teams-js/2.0.0/js/MicrosoftTeams.min.js';
        await app.initialize();
    </script>
...
</body>
```

# <a name="teamsjs-v1"></a>[TeamsJS версии 1](#tab/teamsjs-v1)

```html
<!DOCTYPE html>
<html>
<head>
...
    <script src= 'https://statics.teams.cdn.office.net/sdk/v1.10.0/js/MicrosoftTeams.min.js'></script>
...
</head>

<body>
...
    <script>
    microsoftTeams.initialize();
    </script>
...
</body>
```

***

## <a name="access-additional-content"></a>Доступ к дополнительному содержимому

Вы можете получить доступ к дополнительному содержимому, используя пакет SDK для взаимодействия с Teams, создания глубоких ссылок, использования модулей задач и проверки того, включены ли домены URL в массив `validDomains`.

### <a name="use-the-sdk-to-interact-with-teams"></a>Используйте SDK для взаимодействия с Teams

[Пакет SDK для JavaScript для клиента Teams](~/tabs/how-to/using-teams-client-sdk.md) предоставляет множество дополнительных функций, которые могут оказаться полезными при разработке страницы содержимого.

### <a name="deep-links"></a>Прямые ссылки

Можно создавать прямые ссылки на сущности в Teams. Они используются для создания ссылок, которые переходя к содержимому и сведениям на вкладке. Дополнительные сведения см. в [статье о создании прямых ссылок на содержимое и функции в Teams](~/concepts/build-and-test/deep-links.md).

### <a name="task-modules"></a>Модули задач

Модуль задач — это модальное всплывающее окно, которое можно активировать на вкладке. На странице содержимого используйте модули задач для представления форм для сбора дополнительных сведений, отображения сведений об элементе в списке или представления пользователю дополнительных сведений. Сами модули задач могут быть дополнительными страницами содержимого или полностью создаваться с помощью Adaptive Cards. Дополнительные сведения см. в разделе [Использование модулей задач во вкладках](~/task-modules-and-cards/task-modules/task-modules-tabs.md).

### <a name="valid-domains"></a>Допустимые домены

Убедитесь, что все домены URL, используемые на ваших вкладках, включены в массив `validDomains` вашего [манифеста](~/concepts/build-and-test/apps-package.md). Подробнее см. в разделе [validDomains](~/resources/schema/manifest-schema.md#validdomains) в справочнике по схеме манифеста.

> [!NOTE]
> Основные функции вашей вкладки существуют в Teams, а не за их пределами.

## <a name="show-a-native-loading-indicator"></a>Показать собственный индикатор загрузки

Начиная со [схемы манифеста](../../../resources/schema/manifest-schema.md) версии 1.7, вы можете предоставить [собственный индикатор загрузки](../../../resources/schema/manifest-schema.md#showloadingindicator). Например, [страница содержимого вкладки](#integrate-your-code-with-teams), [страница конфигурации](configuration-page.md), [страница удаления](removal-page.md), и [модули задач на вкладках](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).

> [!NOTE]
>
> * Поведение на мобильных клиентах невозможно настроить с помощью собственного свойства индикатора загрузки. Мобильные клиенты по умолчанию показывают этот индикатор на страницах содержимого и в модулях задач на основе iframe. Этот индикатор на мобильных устройствах отображается, когда делается запрос на получение содержимого, и исчезает, как только запрос выполняется.

Если вы укажете `showLoadingIndicator : true` в манифесте своего приложения, то для всех конфигураций вкладок, содержимое, страниц удаления и всех модулей задач на основе iframe необходимо выполнить следующие шаги:

Чтобы показать индикатор загрузки:

1. Добавьте `"showLoadingIndicator": true` в манифест.
1. вызова метода `app.initialize();`;
1. В качестве **обязательного** шага вызовите `app.notifySuccess()`, чтобы уведомить Teams об успешной загрузке вашего приложения. Затем Teams скрывает индикатор загрузки, если это применимо. Если `notifySuccess`  вызов не выполняется в течение 30 секунд, Teams предполагает, что время ожидания приложения истекло, и отображается экран ошибки с параметром повтора.
1. **При необходимости**, если вы готовы печатать на экране и хотите отложенной загрузки остального содержимого приложения, можно скрыть индикатор загрузки вручную, вызвав его `app.notifyAppLoaded();`.
1. Если приложение не загружается, `app.notifyFailure({reason: app.FailedReason.Timeout, message: "failure message"});` вы можете позвонить в Teams, чтобы узнать о сбое, и при необходимости указать сообщение о сбое. Пользователю показывается экран ошибки. В следующем коде показано перечисление, определяющее возможные причины сбоя загрузки приложения:

    ```typescript
    /* List of failure reasons */
    export const enum FailedReason {
        AuthFailed = "AuthFailed",
        Timeout = "Timeout",
        Other = "Other"
    }
    ```

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Создать страницу конфигурации](~/tabs/how-to/create-tab-pages/configuration-page.md)

## <a name="see-also"></a>Дополнительные ресурсы

* [Вкладки Teams](~/tabs/what-are-tabs.md)
* [Создание личной вкладки](~/tabs/how-to/create-personal-tab.md)
* [Развертывание ссылок вкладок и представление "Сцена"](~/tabs/tabs-link-unfurling.md)
* [Создать страницу конфигурации](~/tabs/how-to/create-tab-pages/configuration-page.md)
* [DevTools для вкладок Microsoft Teams](~/tabs/how-to/developer-tools.md)
