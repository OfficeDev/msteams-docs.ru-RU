---
title: Проектирование приложения с помощью расширенных компонентов пользовательского интерфейса
author: heath-hamilton
description: Сведения о компонентах пользовательского интерфейса Teams, таких как навигация, панель уведомлений, представление стадии, а также соответствующие варианты использования.
ms.author: surbhigupta
ms.localizationpriority: medium
ms.topic: reference
ms.openlocfilehash: d0c95c680e4cbf81776ebe7d5b0a580b5cff7d2d
ms.sourcegitcommit: c1032ea4f48c4bbf5446798ff7d46d7e6e9f55d2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/27/2022
ms.locfileid: "68027349"
---
# <a name="designing-your-microsoft-teams-app-with-advanced-ui-components"></a>Проектирование приложения Microsoft Teams с помощью расширенных компонентов пользовательского интерфейса

Следующие компоненты — это сочетание основных [компонентов](~/concepts/design/design-teams-app-basic-ui-components.md) пользовательского интерфейса, которые можно использовать для распространенных ситуаций проектирования Teams, таких как навигация.

## <a name="microsoft-teams-ui-kit"></a>Комплект разработчика для пользовательского интерфейса Microsoft Teams

На основе [пользовательского интерфейса Fluent](https://fluentsite.z22.web.core.windows.net/) комплект пользовательского интерфейса Microsoft Teams включает компоненты и шаблоны, разработанные специально для создания приложений Teams. В комплекте пользовательского интерфейса можно захватывать и вставлять перечисленные здесь компоненты непосредственно в макет и просматривать дополнительные примеры использования каждого компонента.

> [!div class="nextstepaction"]
> [Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="breadcrumb"></a>Breadcrumb

Навигационные строки — это навигационная структура, которая передает иерархию приложения. Они помогают пользователям понять, как просматриваемая страница соответствует общему интерфейсу, и позволяют одним щелчком получить доступ к более высоким уровням в этой иерархии.

### <a name="top-use-cases"></a>Основные варианты использования

* Связывать иерархию
* Навигация

### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/ui-templates/mobile-breadcrumb.png" alt-text="В примере показан шаблон навигации на мобильных устройствах.":::

### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="Пример шаблона навигации на рабочем столе.":::

## <a name="left-nav"></a>Навигация по левому краю

Используйте левую панель навигации для просмотра нескольких страниц на вкладке Teams. В следующем примере левая панель навигации находится между списком каналов и содержимым вкладки.

### <a name="top-use-cases"></a>Основные варианты использования

* Просмотр нескольких страниц на вкладке Teams.
* Разбивайте сложные приложения на несколько страниц.

### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/ui-templates/mobile-left-nav.png" alt-text="В примере показан левый шаблон навигации на мобильных устройствах.":::

### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="В примере показан левый шаблон навигации на рабочем столе.":::

## <a name="notification-bar"></a>Панель уведомлений

Панель уведомлений — это выделенная область для отображения кратких важных сообщений, которые не требуют от пользователя немедленного выполнения действий. Определенные цвета фона и значки связаны с определенными типами сообщений (см. ниже).

Вы можете реализовать панель уведомлений с помощью компонента оповещений Пользовательского [интерфейса](https://fluentsite.z22.web.core.windows.net/0.59.0/components/alert/definition) Fluent.

### <a name="top-use-cases"></a>Основные варианты использования

* Критические сообщения, ошибки и предупреждения
* Сообщения об успешном выполнении
* Информационные или рекламные сообщения

### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/ui-templates/mobile-notification-bar.png" alt-text="В примере показан шаблон пользовательского интерфейса панели уведомлений на мобильном устройстве.":::

### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="В примере показаны шаблоны пользовательского интерфейса панели уведомлений на рабочем столе.":::

## <a name="stage-view"></a>Представление "Экран"

Представление стадии позволяет пользователям просматривать содержимое ( например, изображение, файл или веб-сайт) на большой поверхности в Teams без переключения контекста. Этот компонент предназначен в основном для просмотра содержимого. Не используйте его для сложных взаимодействий.

Узнайте, как реализовать [представление стадии](~/tabs/tabs-link-unfurling.md).

### <a name="top-use-cases"></a>Основные варианты использования

* Отображение содержимого в большой области в Teams вместо другого приложения или браузера
* Интересное мультимедиа или другое полнофункциональный контент

### <a name="mobile"></a>Мобильная версия

Приложение может запускать этап из адаптивной карточки, общей ссылки или визуальных компонентов (например, диаграммы).

:::image type="content" source="../../assets/images/ui-templates/mobile-stage.png" alt-text="В примере показан шаблон этапа на мобильном устройстве.":::

### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="В примере показан шаблон этапа на рабочем столе.":::

## <a name="toolbar"></a>Панель инструментов

Панель инструментов — это контейнер для группирования набора элементов управления.

### <a name="top-use-cases"></a>Основные варианты использования

* Контекстные действия с содержимым приложения.
* Контекстный фильтр и поиск.
* Навигация и навигация.

### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/ui-templates/mobile-toolbar.png" alt-text="В примере показан шаблон панели инструментов на мобильном устройстве.":::

### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="Пример шаблона панели инструментов на рабочем столе.":::
