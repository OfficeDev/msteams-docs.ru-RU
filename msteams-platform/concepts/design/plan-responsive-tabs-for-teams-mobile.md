---
title: Планирование мобильной версии Teams
author: surbhigupta
description: В этом модуле обучения вы узнаете, как спланировать создание приложения на мобильных устройствах Teams и понять различные этапы создания приложения.
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: v-abirade
ms.openlocfilehash: e7cf4508f723efa1b2a0445d304e080677b257ff
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791561"
---
# <a name="plan-responsive-tabs-for-teams-mobile"></a>Планирование адаптивных вкладок для мобильной версии Teams

 Платформа Teams предоставляет возможность создавать приложения на мобильных устройствах и компьютерах. Пользователи вашего приложения могут применять компьютер или мобильное устройство либо оба варианта. Пользователи могут подготовить данные на компьютере, но использовать данные и делиться ими с помощью мобильных устройств. Ключом к созданию любого приложения является понимание и выполнение потребностей пользователей. Существуют такие возможности, как боты, расширения для сообщений и соединители, которые легко работают на компьютерах и мобильных устройствах. Однако для создания вкладок и модулей задач требуется планирование размещения вашего веб-интерфейса в мобильной версии Teams. В этой статье содержатся инструкции по планированию адаптивных веб-страниц в мобильной версии Teams.

## <a name="identify-apps-scope"></a>Определение области приложений

В следующем списке приведены основные сведения по планированию создания приложений для мобильной версии Teams.

* Учитывайте применение функций приложения Teams на разных устройствах. Например, если у вас есть хорошо работающее приложение на компьютере, вы можете изучить создание аналогичного приложения для мобильных устройств. Изначально может быть сложно перенести весь классический интерфейс в мобильную версию. Вы можете начать с основных, но распространенных сценариев. Добавляйте функции и возможности после сбора дополнительной аналитики и отзывов пользователей.

* В качестве цели используйте соответствующего пользователя на мобильном устройстве. Например, если вы создаете приложение, которое обслуживает конечных пользователей, а также предоставляет доступ к данным для разработчиков и старшего руководства, конечные пользователи могут чаще использовать приложение, когда вы начнете создавать приложение в мобильной версии Teams. Вы можете обслуживать всех пользователей, которые у вас есть в вашем классическом приложении, однако рекомендуется начать с пользователя из более крупной базы и возможными ранними последователями для взаимодействия на небольшом экране. В соответствии с примером конечные пользователи являются соответствующими целевыми пользователями. Вы можете постепенно добавлять функции для поддержки других пользователей в мобильной версии Teams.

## <a name="understand-different-stages-to-build-apps"></a>Общие сведения о различных этапах создания приложений

После определения области приложения пора ознакомиться со следующими тремя этапами планирования любого приложения в мобильной версии Teams и улучшить взаимодействие с пользователем:

1. **Использование**

   Просмотр приложений на мобильных устройствах. Чтобы создать приложение на мобильном устройстве, вы можете начать с интерфейса использования. Так как в мобильном мире прокрутка содержимого является распространенной практикой, вы можете отобразить соответствующую информацию. Используйте механизмы задействования, например уведомления, для информирования об обновлениях.

2. **Быстрые действия**

   Использование приложения на мобильных устройствах. После того как пользователи начинают использовать содержимое на мобильных устройствах, вы можете масштабировать ваше приложение до следующего уровня путем переноса некоторых действий из классического приложения. Вы можете оптимизировать и создать новые действия для мобильных устройств.

3. **Включение**

   Предоставьте полный интерфейс приложения для взаимодействия на мобильных устройствах. По мере того как пользователи взаимодействуют с вашим приложением, предоставляйте полный иммерсивный интерфейс на мобильных устройствах на том же уровне или даже лучше, чем в классическом интерфейсе. Чтобы обеспечить хорошее взаимодействие с пользователями, сделайте все варианты использования адаптивными на мобильных устройствах.

    > [!TIP]
    > Чтобы получить сведения о рекомендациях по разработке, см. статью [Процесс разработки приложений Teams](design-teams-app-process.md).

## <a name="use-cases"></a>Варианты использования

Давайте рассмотрим следующие варианты использования, чтобы понять, как спланировать различные типы приложений для мобильной версии Teams.

<br>

<details>

<summary><b>Панели мониторинга и приложения визуализации данных</b></summary>

Вы можете узнать, как спланировать адаптивные вкладки для панелей мониторинга и приложений визуализации данных на мобильной платформе Teams.

Использование:

На первом этапе вы можете реализовать самый простой интерфейс использования для просмотра данных. Любое приложение в домене предназначено для отображения данных в виде визуализаций. В своем приложении вы можете отображать недавно просмотренные в классической версии визуализации или список всех диаграмм, разрешенных для пользователей. После создания панелей мониторинга в классической версии пользователи могут обращаться к информации с помощью мобильной версии. Вы можете отображать подробное представление любой диаграммы, выбранной пользователем, в виде развернутого представления на вкладках или с помощью модулей задач.

Вы можете указать следующие сведения.

* Панели мониторинга и сводки.
* Визуальные элементы данных, карты и инфографика.
* Диаграммы, графы и таблицы.

:::image type="content" source="../../assets/images/app-fundamentals/dashboarding-and-data-visualization-apps-consumption.png" alt-text="Отображение данных в виде визуализации.":::

Быстрые действия:

На втором этапе пользователи могут работать с существующими диаграммами и визуальными элементами из классического интерфейса. Можно добавить следующие действия.

* Поиск содержимого.
* Фильтрация данных.
* Создание закладок.

:::image type="content" source="../../assets/images/app-fundamentals/dashboarding-and-data-visualization-apps-quick-actions.png" alt-text="Быстрые действия с существующей диаграммой и визуальными элементами.":::

Включение:

На третьем этапе разрешите пользователям создавать содержимое с нуля, например диаграммы и графики. Добавьте все возможности в свое приложение для мобильных устройств. Например, вы можете использовать модули задач для доступа к определенным элементам данных с подробным представлением.

Вы можете предоставить пользователям следующий доступ:

* Измените заголовок и описание.
* Вставка элементов данных для создания визуализаций.
* Предоставление общего доступа к визуализациям в канале или групповом чате.

:::image type="content" source="../../assets/images/app-fundamentals/dashboarding-and-data-visualization-apps-enablement.png" alt-text="Разрешить пользователям создавать содержимое, например графику диаграмм.":::

<br>

</details>

<br>

<details>

<summary><b>Приложения с досками задач</b></summary>

Вы можете узнать, как спланировать адаптивные вкладки для приложений с досками задач на мобильной платформе Teams.

Использование:

На первом этапе ваше приложение может отображать список задач для пользователя в вертикальной стопке. Если существует несколько категорий задач, например **Предложенные**, **Активные** и **Закрытые**, предоставьте фильтры для отображения задач по группам или в виде заголовков для просмотра сгруппированных задач.

:::image type="content" source="../../assets/images/app-fundamentals/taskboarding-apps-consumption.png" alt-text="Показывает список задач в вертикальном стеке.":::

Быстрые действия:

На втором этапе вы можете предоставить пользователям следующий доступ к приложению.

* Создавайте задачи или элементы с обязательными полями для снижения когнитивной нагрузки пользователей.
* Измените тип или представление доски.
* Просмотр задач путем развертывания представления.
* Используйте модули задач для просмотра подробных сведений.
* Переместите задачи в разные категории.
* Делитесь соответствующими задачами в чатах и каналах с помощью электронной почты и веб-канала действий.

:::image type="content" source="../../assets/images/app-fundamentals/taskboarding-apps-quick-actions.png" alt-text="Создание задач для снижения когнитивной нагрузки пользователей.":::

Включение:

На третьем этапе вы можете включить взаимодействие пользователей со следующими действиями.

* Добавление новых проектов и досок.
* Добавьте и измените различные категории, такие как **Предлагаемые**, **Активные** и **Закрытые**.
* Настройте задачи для комментариев, вложений и других сложных функций.

:::image type="content" source="../../assets/images/app-fundamentals/taskboarding-apps-enablement.png" alt-text="Включите взаимодействие с пользователем, добавив проекты и доски.":::

<br>

</details>

<br>

<details>

<summary><b>Приложения совместной работы и демонстрации досок</b></summary>

Вы можете узнать, как спланировать адаптивные вкладки для приложений совместной работы и демонстрации досок на мобильной платформе Teams.

Использование:

На первом этапе можно рассмотреть классические возможности для отображения содержимого и ресурсов в вашем приложении.  Вы можете отобразить следующие функции.

* Комментарии или отзывы.
* Увеличение или уменьшение масштаба.
* Текущий этап или ход выполнения ожидающего документа.

:::image type="content" source="../../assets/images/app-fundamentals/coauthoring-and-whiteboarding-apps-consumption.png" alt-text="Отображает содержимое и ресурсы в интерфейсе рабочего стола.":::

Быстрые действия:

На втором этапе вы можете добавить следующие действия.

* Создайте новую доску для совместной работы или новые документы для подписи.
* Делитесь досками внутри, а также с гостями.
* Настройка разрешений администратора.

> [!TIP]
> Вы предоставляете действия, которые можно легко отображать на небольших экранах.

:::image type="content" source="../../assets/images/app-fundamentals/coauthoring-and-whiteboarding-apps-quick-actions.png" alt-text="Сведения о создании новой доски для совместной работы.":::

Включение:

На третьем этапе предоставьте пользователям полный интерфейс. Вы можете включить взаимодействие пользователей со следующими действиями.

* Добавление текста, фигур и кратких заметок.
* Перемещаться по содержимому.
* Добавление слоев и фильтров.
* Операции удаления, отмены и повтора.
* Доступ к камере и микрофону с помощью API пакета SDK для JS. Дополнительные сведения о возможностях устройств см. в [обзоре возможностей устройств](../device-capabilities/device-capabilities-overview.md).

:::image type="content" source="../../assets/images/app-fundamentals/coauthoring-and-whiteboarding-apps-enablement.png" alt-text="Чтобы обеспечить взаимодействие с пользователем, добавьте текстовые фигуры, краткие заметки и другие возможности.":::

<br>

</details>

## <a name="see-also"></a>Дополнительные ресурсы

Следующие рекомендации по проектированию и проверке помогают в зависимости от области действия вашего приложения.

* [Проектирование вкладки](../../tabs/design/tabs.md)
* [Создание бота](../../bots/design/bots.md)
* [Проектирование модулей задач](../..//task-modules-and-cards/task-modules/design-teams-task-modules.md)
* [Рекомендации по проверке в магазине](../deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)
