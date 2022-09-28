---
title: Решение Teams для создания приложений
author: heath-hamilton
description: Узнайте, как планировать, проектировать, создавать, расширять microsoft 365, тестировать, распространять, монетизировать и интегрировать приложение с Teams.
ms.topic: overview
ms.localizationpriority: high
ms.author: lajanuar
ms.date: 11/02/2021
ms.openlocfilehash: ac4f3a208484a093460a14777a351aa4abc10af7
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100786"
---
# <a name="the-teams-solution"></a>Решение Teams


Платформа Microsoft Teams — это мощная и гибкая платформа для создания приложений для Microsoft Teams. Она предоставляет широкий набор сред разработки и средств для поддержки разработки приложений.

## <a name="the-user-story"></a>Пользовательская История

Вы просмотрели предложения Teams. Теперь вы можете сопоставить их с потребностями пользователей. Давайте вернемся к сценарию.

Разработчик из тур-агентства хочет создать приложение для своих пользователей — путешественников. Приложение должно:

- Проверять и отправлять прогноз погоды путешественникам, зарегистрированным в туристическом агентстве.
- Уведомлять пользователей за день до даты вылета, чтобы они могли составить план.

Разбор и сопоставление требований с функциями Teams:

| Потребности пользователя в приложении | Проверка прогноза | Уведомление перед поездкой | Зарегистрированный пользователь |
| --- |:---:|:---:|:---:|
| **Возможности** | Bot | &nbsp; | &nbsp; |
| **Интеграция** | &nbsp; | &nbsp; | :::image type="icon" source="assets/icons/microsoft-icon.png":::Microsoft Graph, API для прогноза погоды |
| **Scope** | &nbsp; | Личное приложение | &nbsp; |
| **Точка интеграции** | &nbsp; | Чат | &nbsp; |

**Решение для приложения Teams**: Приложение для *личного чата Teams*, которое проверяет и *отправляет уведомление о прогнозе погоды* *зарегистрированным пользователям* до даты их поездки.

:::image type="content" source="../msteams-platform/assets/images/overview/developer-scenario-solution.png" alt-text="Разработчик туристического агентства создает бота для Teams, который отправляет прогноз погоды клиентам, чтобы они могли заранее планировать даты поездки":::

Teams offers these and many more capabilities to bring your users a feature-rich app solution. To develop this app:

1. Создайте приложение для личного чат-бота.
1. Выполните интеграцию с внешним API прогноза погоды для подключения и запроса прогноза для конкретной даты и географического расположения.
1. Интеграция с :::image type="icon" source="assets/icons/teams-icon.png"::: Microsoft Graph для зарегистрированных пользователей.
1. Проверьте и отправьте сведения о прогнозе на основе даты и места поездки пользователя.

## <a name="choose-what-suits-you"></a>Выберите то, что подходит вам

Вы можете создать приложение Teams в соответствии с требованиями вашего приложения. Основываясь на таких факторах, как бизнес-потребности, среда разработки, знание домена, выберите среду и инструменты, которые вы хотите создать для своего приложения.

Приложение Teams позволяет выбрать среду сборки. Это включает инструменты, инфраструктуру и языки для разработки приложений.

:::image type="content" source="../msteams-platform/assets/images/overview/tools-of-your-choice.png" alt-text="Приложение для бизнеса":::

Build your Teams app in the environment that works for your particular requirements. You can even select a combination.

Например, с помощью набора средств Teams можно создать приложение с помощью JavaScript и разместить его на сайте SharePoint.

## <a name="teams-collaborative-platform"></a>Платформа для совместной работы в Teams

Приложение Teams дает пользователям преимущества рабочего пространства для совместной работы.

В качестве платформы для создания приложений Teams предлагает полный набор приложений и наборов средств. Платформа Teams поддерживает вас на каждом этапе от планирования приложения до его распространения.

:::image type="content" source="../msteams-platform/assets/images/overview/teams-dev-life-cycle.png" alt-text="Описание жизненного цикла разработки приложений Teams. Планирование, проектирование, сборка, расширение, тестирование, развертывание, распространение. Сведения показаны в маркированном списке ниже.":::

From designing to building and distributing a Teams app, you can use various tools and services. An example development flow can be:

1. Планирование проекта и выявление требований.
1. Design the app. Use Teams UI Kit and UI Library for designing tabs UI.
1. Создание приложения с помощью JavaScript с использованием набора средств Teams.
1. Расширяйте функциональность, добавляя дополнительные возможности Teams и данные M365 с помощью :::image type="icon" source="assets/icons/microsoft-icon.png":::Microsoft Graph.
1. Тестирование приложения в клиенте разработчика с примерами пользовательских данных.
1. Развертывание приложения в Azure.
1. Управление приложениями и их публикация в Store с помощью Портала разработчика. Монетизируйте свое приложение с помощью таких вариантов, как предложения SaaS, покупки в приложении и т. д.

## <a name="next-step"></a>Следующий этап

:::row:::
    :::column span="1":::
        **Начало разработки**
    :::column-end:::
    :::column span="2":::
        Ознакомьтесь с разработкой для Teams, настроив среду и создав простое приложение.

        > [!div class="nextstepaction"]
        > [Создание первого приложения](get-started/get-started-overview.md)
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>См. также

:::row:::
    :::column span="1":::
        **Планирование приложения**
    :::column-end:::
    :::column span="2":::
        Изучите и сопоставьте варианты использования вашего приложения с функциями Teams.

        > [!div class="nextstepaction"]
        > [Планирование приложения](~/concepts/app-fundamentals-overview.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **Создание приложения**
    :::column-end:::
    :::column span="2":::
        Создайте пользовательский интерфейс приложения с помощью Teams UI Kit.

        > [!div class="nextstepaction"]
        > [Разработка приложения Microsoft Teams](~/concepts/design/design-teams-app-process.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **Создание приложения**
    :::column-end:::
    :::column span="2":::
        Looking for app development inspiration? Browse our list of real-world scenarios and industry solutions with high fidelity concept mocks to understand the various ways a Teams app can help your users.

        > [!div class="nextstepaction"]
        > [См. сценарии приложений](https://adoption.microsoft.com/en-us/extensibility-look-book-gallery/)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **Расширение приложения в Microsoft 365**
    :::column-end:::
    :::column span="2":::
Вы можете просмотреть свои приложения Teams, работающие в других активно используемых средах Microsoft 365, с помощью Teams JavaScript Client SDK v2 Preview.

        > [!div class="nextstepaction"]
        > [Расширение приложения](m365-apps/overview.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **Тестирование приложения**
    :::column-end:::
    :::column span="2":::
        После интеграции вашего приложения с Teams вы должны протестировать свое приложение перед его публикацией.

        > [!div class="nextstepaction"]
        > [Тестирование приложения](concepts/build-and-test/test-app-overview.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **Распространение приложения**
    :::column-end:::
    :::column span="2":::
        Вы можете предоставить свое приложение Teams отдельному лицу, команде, организации или всем, кто хочет его использовать.

        > [!div class="nextstepaction"]
        > [Распространение приложения](~/concepts/deploy-and-publish/apps-publish-overview.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **Монетизация приложения**
    :::column-end:::
    :::column span="2":::
        Магазин Teams предлагает варианты монетизации приложений, например предложения SaaS и покупки в приложении. Выберите оптимальный вариант монетизации, подходящий для вашего приложения Teams.

        > [!div class="nextstepaction"]
        > [Монетизация приложения](concepts/deploy-and-publish/appsource/prepare/monetize-overview.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **Интеграция с Teams**
    :::column-end:::
    :::column span="2":::
        Совмещайте функции, которые нравятся пользователям в существующем веб-приложении, службе или системе с функциями совместной работы Microsoft Teams.

        > [!div class="nextstepaction"]
        > [Интеграция существующего приложения](samples/integrating-web-apps.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **Немного кода — много возможностей**
    :::column-end:::
    :::column span="2":::
        You don't need to be an expert programmer to build a great Teams app. Try one of several low-code solutions.

        > [!div class="nextstepaction"]
        > [Создание приложений с малым использованием кода](samples/teams-low-code-solutions.md)
    :::column-end:::
:::row-end:::
