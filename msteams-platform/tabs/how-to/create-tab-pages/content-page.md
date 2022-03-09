---
title: Создать страницу контента
author: surbhigupta
description: создание страницы контента
keywords: группы вкладок группового канала, настраиваемые статическими
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 887559b65acd7c28ba6c8f96b380fde837fbc053
ms.sourcegitcommit: 830fdc80556a5fde642850dd6b4d1b7efda3609d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/09/2022
ms.locfileid: "63398591"
---
# <a name="create-a-content-page-for-your-tab"></a>Создание страницы контента для вкладки

Страница контента — это веб-страница, отрисовка в Teams клиенте. Они являются частью:

* Настраиваемая вкладка с личным охватом. В этом случае страница контента является первой страницей, с которой сталкивается пользователь.
* Настраиваемая вкладка канала или группы. Страница контента отображается после пин-кодов пользователя и настраивает вкладку в соответствующем контексте.
* Модуль [задач](~/task-modules-and-cards/what-are-task-modules.md). Вы можете создать страницу контента и встраить ее в веб-просмотр внутри модуля задач. Страница отрисовка в модальной всплываемой области.

Эта статья посвящена использованию страниц контента в качестве вкладок; однако большинство указаний здесь применяется независимо от того, как страница контента представлена пользователю.

## <a name="tab-content-and-design-guidelines"></a>Рекомендации по контенту и дизайну вкладок

Общая цель вкладки — предоставить доступ к содержательному и привлекательному контенту, который имеет практическое значение и очевидная цель. Необходимо сосредоточиться на том, чтобы сделать дизайн вкладки чистым, интуитивно понятным и захватывающим контентом.

Дополнительные сведения см. в [руководстве](~/tabs/design/tabs.md) по разработке вкладок [Microsoft Teams руководства](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) по проверке хранения.

## <a name="integrate-your-code-with-teams"></a>Интеграция кода с Teams

Чтобы ваша страница отображалась в Teams, необходимо включить Microsoft Teams [клиента JavaScript и](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.initialize()` включить вызов после загрузки страницы.

В следующем коде приводится пример взаимодействия вашей страницы и Teams клиента:

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

## <a name="access-additional-content"></a>Доступ к дополнительному контенту

Вы можете получить доступ к дополнительному контенту с помощью SDK для взаимодействия с Teams, создания глубоких ссылок, `validDomains` использования модулей задач и проверки того, включены ли url-домены в массив.

### <a name="use-the-sdk-to-interact-with-teams"></a>Используйте SDK для взаимодействия с Teams

[Клиентская Teams JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md) предоставляет множество дополнительных функций, которые можно найти полезными при разработке страницы контента.

### <a name="deep-links"></a>Прямые ссылки

Можно создавать прямые ссылки на сущности в Teams. Они используются для создания ссылок, которые переходят к содержимому и сведениям в вкладке. Дополнительные сведения см. в [дополнительных сведениях о создании глубоких](~/concepts/build-and-test/deep-links.md) ссылок на контент и функции в Teams.

### <a name="task-modules"></a>Модули задач

Модуль задач — это модуль всплывающих модулей, который можно запускать с вкладки. На странице контента можно использовать модули задач для отображения форм для сбора дополнительных сведений, отображения сведений о элементе в списке или для получения дополнительных сведений. Сами модули задач могут быть дополнительными страницами контента или полностью создаваться с помощью адаптивных карт. Дополнительные сведения см. в [таблицах с использованием модулей задач](~/task-modules-and-cards/task-modules/task-modules-tabs.md).

### <a name="valid-domains"></a>Допустимые домены

Убедитесь, что все URL-домены, используемые в вкладке, включены в массив `validDomains` [манифеста](~/concepts/build-and-test/apps-package.md). Дополнительные сведения см. [в справке по схеме манифеста validDomains](~/resources/schema/manifest-schema.md#validdomains) .

> [!NOTE]
> Основные функции вкладки существуют в Teams, а не за пределами Teams.

## <a name="show-a-native-loading-indicator"></a>Показать индикатор загрузки

Начиная с [схемы манифеста v1.7](../../../resources/schema/manifest-schema.md), можно [предоставить индикатор](../../../resources/schema/manifest-schema.md#showloadingindicator) загрузки. Например, страница [контента вкладок](#integrate-your-code-with-teams), [страница конфигурации](configuration-page.md), [страница удаления](removal-page.md) и модули [задач на вкладке](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).

> [!NOTE]
>
> * Поведение мобильных клиентов не настраивается с помощью свойства индикатора загрузки. Мобильные клиенты по умолчанию показывают этот индикатор на страницах контента и модулях задач на основе iframe. Этот индикатор на мобильном телефоне отображается при запросе на извлечение контента и его отклонять сразу же после завершения запроса.

Если вы указываете `showLoadingIndicator : true`  в манифесте приложения, то все конфигурации вкладок, содержимое, страницы удаления и все модули задач на основе iframe должны следовать следующим шагам:

Чтобы показать индикатор загрузки:

1. Добавьте `"showLoadingIndicator": true` в манифест.
1. вызова метода `microsoftTeams.initialize();`;
1. В качестве **обязательного шага** позвоните, `microsoftTeams.appInitialization.notifySuccess()` чтобы уведомить Teams, что ваше приложение успешно загружено. Teams затем скрывает индикатор загрузки, если это применимо. Если `notifySuccess`  не вызвано в течение 30 секунд, предполагается, что ваше приложение ото времени и появится экран ошибок с параметром повторной проверки.
1. **Необязательно,** если вы готовы печатать на экране и хотите полениться загрузить остальную часть контента приложения, `microsoftTeams.appInitialization.notifyAppLoaded();`вы можете вручную скрыть индикатор загрузки, позвонив .
1. Если приложение не загружается, `microsoftTeams.appInitialization.notifyFailure(reason);` можно позвонить, чтобы Teams, что произошла ошибка. Экран ошибки отображается пользователю. В следующем коде приводится пример причин отказа приложения:

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

## <a name="see-also"></a>См. также

* [Teams вкладки](~/tabs/what-are-tabs.md)
* [Создание личной вкладки](~/tabs/how-to/create-personal-tab.md)
* [Предварительный просмотр для ссылки "Вкладки" и представление стадий](~/tabs/tabs-link-unfurling.md)
* [Создать страницу конфигурации](~/tabs/how-to/create-tab-pages/configuration-page.md)
* [DevTools для вкладок Microsoft Teams](~/tabs/how-to/developer-tools.md)
