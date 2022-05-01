---
title: Создать страницу контента
author: surbhigupta
description: как создать страницу содержимого
keywords: настраиваемый канал группы вкладок Teams
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 68ce03e9b1ef303bd66043baed39baf954fb1d0f
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111432"
---
# <a name="create-a-content-page-for-your-tab"></a>Создание страницы содержимого для вкладки

Страница содержимого — это веб-страница, отображаемая в клиенте Teams. Они являются частью:

* Настраиваемая вкладка с личной областью действия: в этом случае страница содержимого — это первая страница, с которой сталкивается пользователь.
* Настраиваемая вкладка канала или группы: страница содержимого отображается после того, как пользователь закрепит и настроит вкладку в соответствующем контексте.
* [Модуль задач](~/task-modules-and-cards/what-are-task-modules.md): вы можете создать страницу содержимого и встроить ее как веб-представление в модуль задач. Страница отображается внутри модального всплывающего окна.

Эта статья посвящена использованию страниц содержимого в качестве вкладок; однако большинство этих рекомендаций применимы независимо от того, как страница содержимого представлена ​​пользователю.

## <a name="tab-content-and-design-guidelines"></a>Содержимое вкладок и рекомендации по дизайну

Общая цель вкладки — предоставить доступ к значимому и увлекательному контенту, имеющему практическую ценность и очевидную цель. Необходимо сосредоточиться на чистоте дизайна вкладок, интуитивной навигации и иммерсивном содержимом.

Подробнее см. в [Рекомендациях по дизайну вкладок](~/tabs/design/tabs.md) и [Рекомендациях по проверке хранилища Microsoft Teams](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md).

## <a name="integrate-your-code-with-teams"></a>Интегрируйте свой код с Teams

Чтобы страница отображалась в Teams, нужно включить [клиентский SDK Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) для JavaScript и включить вызов `microsoftTeams.initialize()` после загрузки страницы.

В следующем коде показан пример взаимодействия вашей страницы и клиента Teams.

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

## <a name="access-additional-content"></a>Доступ к дополнительному содержимому

Вы можете получить доступ к дополнительному содержимому, используя пакет SDK для взаимодействия с Teams, создания глубоких ссылок, использования модулей задач и проверки того, включены ли домены URL в массив `validDomains`.

### <a name="use-the-sdk-to-interact-with-teams"></a>Используйте SDK для взаимодействия с Teams

[Пакет SDK для JavaScript для клиента Teams](~/tabs/how-to/using-teams-client-sdk.md) предоставляет множество дополнительных функций, которые могут оказаться полезными при разработке страницы содержимого.

### <a name="deep-links"></a>Прямые ссылки

Можно создавать прямые ссылки на сущности в Teams. СОни используются для создания ссылок, которые ведут к содержимому и информации на вашей вкладке. Дополнительные сведения см. в статье [Создание глубоких ссылок на содержимое и функции в Teams](~/concepts/build-and-test/deep-links.md).

### <a name="task-modules"></a>Модули задач

Модуль задач — это модальное всплывающее окно, которое вы можете активировать на своей вкладке. На странице содержимого вы можете использовать модули задач для представления форм для сбора дополнительных сведений, отображения сведений об элементе в списке или предоставления дополнительных сведений пользователю. Сами модули задач могут быть дополнительными страницами содержимого или полностью создаваться с помощью Adaptive Cards. Дополнительные сведения см. в разделе [Использование модулей задач во вкладках](~/task-modules-and-cards/task-modules/task-modules-tabs.md).

### <a name="valid-domains"></a>Допустимые домены

Убедитесь, что все домены URL, используемые на ваших вкладках, включены в массив `validDomains` вашего [манифеста](~/concepts/build-and-test/apps-package.md). Подробнее см. в разделе [validDomains](~/resources/schema/manifest-schema.md#validdomains) в справочнике по схеме манифеста.

> [!NOTE]
> Основные функции вашей вкладки существуют в Teams, а не за их пределами.

## <a name="show-a-native-loading-indicator"></a>Показать собственный индикатор загрузки

Начиная со [схемы манифеста](../../../resources/schema/manifest-schema.md) версии 1.7, вы можете предоставить [собственный индикатор загрузки](../../../resources/schema/manifest-schema.md#showloadingindicator). Например, [страница содержимого вкладки](#integrate-your-code-with-teams), [страница конфигурации](configuration-page.md), [страница удаления](removal-page.md), и [модули задач на вкладках](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).

> [!NOTE]
>
> * Поведение в мобильных клиентах не настраивается с помощью собственного свойства индикатора загрузки. Мобильные клиенты по умолчанию показывают этот индикатор на страницах содержимого и в модулях задач на основе iframe. Этот индикатор на мобильных устройствах отображается, когда делается запрос на получение содержимого, и исчезает, как только запрос выполняется.

Если вы укажете `showLoadingIndicator : true` в манифесте своего приложения, то для всех конфигураций вкладок, содержимое, страниц удаления и всех модулей задач на основе iframe необходимо выполнить следующие шаги:

Чтобы показать индикатор загрузки:

1. Добавьте `"showLoadingIndicator": true` в манифест.
1. вызова метода `microsoftTeams.initialize();`;
1. В качестве **обязательного** шага вызовите `microsoftTeams.appInitialization.notifySuccess()`, чтобы уведомить Teams об успешной загрузке вашего приложения. Затем Teams скрывает индикатор загрузки, если это применимо. Если `notifySuccess` не вызывается в течение 30 секунд, предполагается, что время ожидания вашего приложения истекло, и появляется экран ошибки с возможностью повторной попытки.
1. **При желании**, если вы готовы печатать на экране и хотите отложить загрузку остального содержимого приложения, вы можете вручную скрыть индикатор загрузки, вызвав метод `microsoftTeams.appInitialization.notifyAppLoaded();`.
1. Если не удается загрузить приложение, вы можете вызвать `microsoftTeams.appInitialization.notifyFailure(reason);`, чтобы сообщить Teams об ошибке. Пользователю показывается экран ошибки. В следующем коде приведен пример причин сбоя приложения:

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
