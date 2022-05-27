---
title: Модули задач
author: surbhigupta
description: Добавление модальных всплывающих элементов для сбора и отображения сведений для пользователей из Microsoft Teams приложений
ms.localizationpriority: medium
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: a7d7778aa4d38dbc879255c449b93590d04f00e2
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2022
ms.locfileid: "65756599"
---
# <a name="task-modules"></a>Модули задач

Модули задач дают возможность создавать модальные всплывающие окна в приложении Teams. Во всплывающем окне можно:

* Выполнение собственного пользовательского кода HTML или JavaScript.
* Отображение мини-приложения `<iframe>`на основе, например YouTube или Microsoft Stream видео.
* Отображение [адаптивной карточки](/adaptive-cards/).

Модули задач полезны для инициализации и выполнения задач или отображения подробных сведений, таких как видео или панели мониторинга Power Business Intelligence (BI). Всплывающее окно часто более естественно для пользователей, инициируемых и выполняемых задач, по сравнению с вкладкой или взаимодействием с ботом на основе бесед.

Модули задач создаются на основе Microsoft Teams вкладок. По сути, это вкладка во всплывающем окне. Они используют тот же пакет SDK, поэтому если вы создали вкладку, вы уже знакомы с созданием модуля задач.

Модули задач можно вызывать тремя способами:

* Каналы или личные вкладки. С помощью пакета SDK Microsoft Teams Tabs можно вызывать модули задач из кнопок, ссылок или меню на вкладке. Дополнительные сведения см. [в статье об использовании модулей задач на вкладке](~/task-modules-and-cards/task-modules/task-modules-tabs.md).
* Боты: использование кнопок на [карточках,](~/task-modules-and-cards/cards/cards-reference.md) отправленных от бота. Это полезно, если не требуется, чтобы все пользователи канала могли видеть, что вы делаете с ботом. Например, когда пользователи отвечают на опрос в канале, не рекомендуется просматривать запись этого опроса. Дополнительные сведения см. [в статье об использовании модулей задач Teams ботов](~/task-modules-and-cards/task-modules/task-modules-bots.md).
* За пределами Teams по прямой ссылке: вы также можете создавать URL-адреса для вызова модуля задачи из любого места. Дополнительные сведения см. в [описании синтаксиса глубокой компоновки модуля задач](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax).

## <a name="components-of-a-task-module"></a>Компоненты модуля задач

Вот как выглядит модуль задач при вызове из бота:

:::image type="content" source="../assets/images/task-module/task-module-example.png" alt-text="Пример модуля задач":::

Модуль задачи включает в себя следующее, как показано на предыдущем рисунке:

1. Значок [приложения`color`.](~/resources/schema/manifest-schema.md#icons)
2. Имя [приложения`short`](~/resources/schema/manifest-schema.md#name).
3. Заголовок модуля задачи, указанный в свойстве `title` объекта [TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object).
4. Кнопка закрытия или отмены модуля задач. Если пользователь нажмет эту кнопку, приложение получит `err` событие. Дополнительные сведения см [. в примере отправки результата модуля задачи](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module).

    > [!NOTE]
    > В настоящее время невозможно обнаружить событие `err` при вызове модуля задачи из бота.

5. Синий прямоугольник — это `url` место, где отображается веб-страница при загрузке собственной веб-страницы с помощью свойства объекта [TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object). Дополнительные сведения см. в статье об [определении размера модулей задач](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-sizing).
6. При отображении адаптивной `card` карточки с помощью свойства объекта [TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) добавляется заполнение. Дополнительные сведения см. в [CSS модуля задач для модулей задач HTML или JavaScript](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-css-for-html-or-javascript-task-modules).
7. Кнопки адаптивной карточки отображаются после выбора параметра **"Зарегистрироваться"**. При использовании собственной страницы создайте собственные кнопки.

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Вызов и закрытие модулей задач](~/task-modules-and-cards/task-modules/invoking-task-modules.md)

## <a name="see-also"></a>Дополнительные ресурсы

[Карточки](~/task-modules-and-cards/what-are-cards.md)
