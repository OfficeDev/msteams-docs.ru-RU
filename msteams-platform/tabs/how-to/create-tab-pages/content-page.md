---
title: Создать страницу контента
author: surbhigupta
description: Узнайте о веб-странице в клиенте Teams и является частью личной, канала или настраиваемой вкладки группы. Создайте страницу содержимого и вставьте ее в виде веб-представления в модуль задач.
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 5dcc46567e14d183437982c7ffde26528c836810
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791540"
---
# <a name="create-a-content-page"></a>Создать страницу контента

Страница содержимого — это веб-страница, которая отображается в клиенте Teams, который является частью:

* Настраиваемая вкладка с личной областью действия: в этом случае страница содержимого — это первая страница, с которой сталкивается пользователь.
* Настраиваемая вкладка канала или группы: страница содержимого отображается после того, как пользователь закрепит и настроит вкладку в соответствующем контексте.
* [Модуль задач](~/task-modules-and-cards/what-are-task-modules.md): вы можете создать страницу содержимого и встроить ее как веб-представление в модуль задач. Страница отображается внутри модального всплывающего окна.

Эта статья посвящена использованию страниц содержимого в качестве вкладок; однако большая часть приведенных здесь рекомендаций применяется независимо от того, как страница содержимого представлена пользователю.

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="tab-content-and-design-guidelines"></a>Содержимое вкладок и рекомендации по дизайну

Общая цель вкладки — предоставить доступ к содержательному и привлекательному содержимому, которое имеет практическую ценность и очевидную цель.

Необходимо сосредоточиться на том, чтобы сделать дизайн вкладок чистым, интуитивно понятной навигацией и иммерсивным содержимым. Дополнительные сведения см. в [разделах Рекомендации по проектированию вкладок](~/tabs/design/tabs.md) и [Рекомендации по проверке магазина Microsoft Teams](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md).

## <a name="integrate-your-code-with-teams"></a>Интегрируйте свой код с Teams

Чтобы страница отображалась в Teams, нужно включить [клиентский SDK Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) для JavaScript и включить вызов `app.initialize()` после загрузки страницы.

> [!NOTE]
> Любое изменение содержимого или пользовательского интерфейса в приложении вкладки из-за кэша занимает около 24–48 часов.

В следующем коде показан пример взаимодействия вашей страницы и клиента Teams.

# <a name="teamsjs-v2"></a>[TeamsJS версии 2](#tab/teamsjs-v2)

```html
<!DOCTYPE html>
<html>
<head>
...
    <script src="https://res.cdn.office.net/teams-js/2.2.0/js/MicrosoftTeams.min.js" 
      integrity="sha384yBjE++eHeBPzIg+IKl9OHFqMbSdrzY2S/LW3qeitc5vqXewEYRWegByWzBN/chRh" 
      crossorigin="anonymous" >
    </script>
...
</head>
<body>
...
    <script>
    microsoftTeams.app.initialize();
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

[Пакет SDK для JavaScript для клиента Teams](~/tabs/how-to/using-teams-client-sdk.md) предоставляет множество других функций, которые можно найти полезными при разработке страницы содержимого.

### <a name="deep-links"></a>Прямые ссылки

Можно создавать прямые ссылки на сущности в Teams. Они используются для создания ссылок, которые переходят к содержимому и сведениям на вкладке. Дополнительные сведения см. [в статье Создание глубоких ссылок на содержимое и функции в Teams](~/concepts/build-and-test/deep-links.md).

### <a name="task-modules"></a>Модули задач

Модуль задач — это модальное всплывающее окно, которое можно активировать на вкладке. На странице содержимого используйте модули задач для представления форм для сбора дополнительных сведений, отображения сведений об элементе в списке или представления пользователю дополнительных сведений. Сами модули задач могут быть дополнительными страницами содержимого или создаваться полностью с помощью адаптивных карточек. Дополнительные сведения см. в разделе [Использование модулей задач во вкладках](~/task-modules-and-cards/task-modules/task-modules-tabs.md).

### <a name="valid-domains"></a>Допустимые домены

Убедитесь, что все домены URL, используемые на ваших вкладках, включены в массив `validDomains` вашего [манифеста](~/concepts/build-and-test/apps-package.md). Подробнее см. в разделе [validDomains](~/resources/schema/manifest-schema.md#validdomains) в справочнике по схеме манифеста.

> [!NOTE]
> Основные функции вашей вкладки существуют в Teams, а не за их пределами.

## <a name="show-a-native-loading-indicator"></a>Показать собственный индикатор загрузки

Начиная со [схемы манифеста](../../../resources/schema/manifest-schema.md) версии 1.7, вы можете предоставить [собственный индикатор загрузки](../../../resources/schema/manifest-schema.md#showloadingindicator). Например, [страница содержимого вкладки](#integrate-your-code-with-teams), [страница конфигурации](configuration-page.md), [страница удаления](removal-page.md), и [модули задач на вкладках](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).

> [!NOTE]
>
> Поведение на мобильных клиентах не настраивается с помощью собственного свойства индикатора загрузки. Мобильные клиенты по умолчанию показывают этот индикатор на страницах содержимого и в модулях задач на основе iframe. Этот индикатор на мобильных устройствах отображается, когда делается запрос на получение содержимого, и исчезает, как только запрос выполняется.

Если вы укажете `showLoadingIndicator : true` в манифесте своего приложения, то для всех конфигураций вкладок, содержимое, страниц удаления и всех модулей задач на основе iframe необходимо выполнить следующие шаги:

Чтобы показать индикатор загрузки:

1. Добавьте `"showLoadingIndicator": true` в манифест.
1. вызова метода `app.initialize();`;
1. В качестве **обязательного** шага вызовите `app.notifySuccess()`, чтобы уведомить Teams об успешной загрузке вашего приложения. Затем Teams скрывает индикатор загрузки, если применимо. Если `notifySuccess`  не вызывается в течение 30 секунд, Teams предполагает, что время ожидания вашего приложения истекло, и отображает экран ошибки с параметром повтора.
1. **При необходимости**, если вы готовы к печати на экране и хотите отложенно загрузить остальное содержимое приложения, можно скрыть индикатор загрузки вручную, вызвав .`app.notifyAppLoaded();`
1. Если приложение не загружается, вы можете позвонить `app.notifyFailure({reason: app.FailedReason.Timeout, message: "failure message"});` , чтобы сообщить Teams о сбое и при необходимости предоставить сообщение об ошибке. `notifyFailure` не отображает пользовательское сообщение. Пользователю показывается экран ошибки. В следующем коде показано перечисление, определяющее возможные причины сбоя загрузки приложения:

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
