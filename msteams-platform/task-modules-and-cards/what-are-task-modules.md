---
title: Модули задач
author: surbhigupta
description: Добавьте модули всплывающих приложений для сбора или отображения данных пользователям из Microsoft Teams приложений
localization_priority: Normal
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 3b0e639acc8901a3637189e435fcfc159e992ae3a674a437733474087103193c
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2021
ms.locfileid: "57707684"
---
# <a name="task-modules"></a>Модули задач

Модули задач позволяют создавать модальные всплывающие опытом в Teams приложении. Во всплывающее всплыв

* Запустите собственный пользовательский КОД HTML или JavaScript.
* Покажите `<iframe>` виджет на основе, например видео YouTube или Microsoft Stream.
* Отображение [адаптивной карты](/adaptive-cards/).

Модули задач полезны для инициирования и выполнения задач или отображения богатых сведений, таких как видео или панели мониторинга бизнес-аналитики Power Business (BI). Всплывающее впечатление часто является более естественным для пользователей, инициалов и выполнения задач по сравнению с вкладками или на основе беседы бота.

Модули задач строятся на основе Microsoft Teams вкладок. По сути, это вкладка в окне всплывающее окно. Они используют один и тот же SDK, поэтому если вы создали вкладку, вы уже знакомы с созданием модуля задач.

Модули задач можно вызывать тремя способами:

* Каналы или личные вкладки. С помощью Microsoft Teams вкладок SDK можно вызывать модули задач из кнопок, ссылок или меню на вкладке. Дополнительные сведения см. в [таблицах с использованием модулей задач.](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
* Bots. Использование кнопок на [карточках,](~/task-modules-and-cards/cards/cards-reference.md) отправленных из бота. Это полезно, если не требуется, чтобы все в канале видели, что вы делаете с ботом. Например, когда пользователи отвечают на опрос в канале, не полезно видеть запись создаемого опроса. Дополнительные сведения см. в дополнительных сведениях об использовании модулей задач [от Teams ботов.](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* Вне Teams ссылки: можно также создавать URL-адреса для вызова модуля задач из любой точки. Дополнительные сведения см. в синтаксис [глубокой](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax)ссылки модуля задач .

## <a name="components-of-a-task-module"></a>Компоненты модуля задач

Вот как выглядит модуль задач при вызове с бота:

![Пример модуля задач](~/assets/images/task-module/task-module-example.png)

Модуль задач включает в себя следующее, как показано на предыдущем изображении:

1. Значок [ `color` приложения](~/resources/schema/manifest-schema.md#icons).
2. Имя [ `short` приложения.](~/resources/schema/manifest-schema.md#name)
3. Название модуля задач, указанное в `title` свойстве объекта [TaskInfo.](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object)
4. Кнопка закрыть или отменить модуль задач. Если пользователь выбирает эту кнопку, приложение получает `err` событие. Дополнительные сведения [см. в примере отправки результатов модуля задач.](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module)

    > [!NOTE]
    > В настоящее время невозможно обнаружить событие, когда модуль задач `err` вызывается из бота.

5. Синий прямоугольник — это место, на котором отображается веб-страница, если вы загружаете собственную веб-страницу с помощью свойства `url` [объекта TaskInfo.](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) Дополнительные сведения см. [в деле размеров модуля задач.](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-sizing)
6. Если вы отображаете адаптивную карту с помощью свойства объекта `card` [TaskInfo,](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) для вас добавляется обивка. Дополнительные сведения см. в [cSS-модуле CSS для модулей задач HTML или JavaScript.](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-css-for-html-or-javascript-task-modules)
7. Кнопки адаптивной карты отрисовываются после выбора **регистрации.** При использовании собственной страницы создайте собственные кнопки.

## <a name="see-also"></a>См. также

[Карточки](~/task-modules-and-cards/what-are-cards.md)

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Вызов и закрытие модулей задач](~/task-modules-and-cards/task-modules/invoking-task-modules.md)
