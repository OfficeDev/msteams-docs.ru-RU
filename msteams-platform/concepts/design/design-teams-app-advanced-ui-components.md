---
title: Разработка приложения с помощью расширенных компонентов пользовательского интерфейса
author: heath-hamilton
description: Узнайте о компонентах пользовательского интерфейса, используемых в Teams.
ms.author: surbhigupta
ms.localizationpriority: medium
ms.topic: reference
ms.openlocfilehash: 2e35b83e66e26155b847ad7cb914c1970397676b
ms.sourcegitcommit: 22c9e44437720d30c992a4a3626a2a9f745983c1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2021
ms.locfileid: "60719849"
---
# <a name="designing-your-microsoft-teams-app-with-advanced-ui-components"></a>Разработка приложения Microsoft Teams с расширенными компонентами пользовательского интерфейса

Следующие компоненты — это сочетание базовых [компонентов пользовательского](~/concepts/design/design-teams-app-basic-ui-components.md) интерфейса, которые можно использовать для общих Teams проектирования, таких как навигация.

## <a name="microsoft-teams-ui-kit"></a>Комплект разработчика для пользовательского интерфейса Microsoft Teams

На основе <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent</a>пользовательского интерфейса Microsoft Teams набор пользовательского интерфейса включает компоненты и шаблоны, разработанные специально для Teams приложений. В наборе пользовательского интерфейса можно захватить и вставить компоненты, перечисленные здесь непосредственно в дизайн, и увидеть дополнительные примеры использования каждого компонента.

> [!div class="nextstepaction"]
> [Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="breadcrumb"></a>Breadcrumb

Breadcrumbs — это навигационный помощник, который передает иерархию приложения. Они помогают пользователям понять, как просматриваемая страница вписывается в общий опыт и позволяет одним щелчком мыши получить доступ к более высоким уровням в этой иерархии.

### <a name="top-use-cases"></a>Верхние случаи использования

* Иерархия связи
* Навигация

### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/ui-templates/mobile-breadcrumb.png" alt-text="В примере показан шаблон breadcrumb на мобильных устройствах." border="false":::

### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="В примере показан шаблон breadcrumb на рабочем столе." border="false":::

## <a name="left-nav"></a>Левый nav

Используйте левый nav для просмотра нескольких страниц в Teams вкладке. В следующем примере левый nav находится между списком каналов и контентом вкладок.

### <a name="top-use-cases"></a>Верхние случаи использования

* Просмотрите несколько страниц в Teams вкладке.
* Разбить сложные приложения на несколько страниц.

### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/ui-templates/mobile-left-nav.png" alt-text="В примере показан левый шаблон nav на мобильных устройствах." border="false":::

### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="В примере показан левый шаблон nav на рабочем столе." border="false":::

## <a name="notification-bar"></a>Панель уведомлений

Панели уведомлений — это выделенная область для отображения кратких важных сообщений, не требующих от пользователя немедленных действий. Определенные фоновые цвета и значки связаны с определенными типами сообщений (см. ниже).

### <a name="top-use-cases"></a>Верхние случаи использования

* Критически важные сообщения, ошибки и предупреждения
* Сообщения об успехе
* Информационные или рекламные сообщения

### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/ui-templates/mobile-notification-bar.png" alt-text="В примере показан шаблон пользовательского интерфейса панели уведомлений на мобильных устройствах." border="false":::

### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="В примере показаны шаблоны пользовательского интерфейса панели уведомлений на рабочем столе." border="false":::

## <a name="stage-view"></a>Представление stage

Представление stage позволяет пользователям просматривать контент, например изображение, файл или веб-сайт, на большой поверхности в Teams без переключения контекста. Этот компонент предназначен в первую очередь для просмотра контента. Не используйте его для сложных взаимодействий.

Узнайте, как реализовать [представление сцены.](~/tabs/tabs-link-unfurling.md)

### <a name="top-use-cases"></a>Верхние случаи использования

* Отображение контента на большой поверхности в Teams вместо другого приложения или браузера
* Прожектор мультимедиа или другой контент с богатыми данными

### <a name="mobile"></a>Мобильная версия

Ваше приложение может запускать этап из адаптивной карты, общих ссылок или визуальных компонентов (например, диаграммы).

:::image type="content" source="../../assets/images/ui-templates/mobile-stage.png" alt-text="В примере показан шаблон сцены на мобильных устройствах." border="false":::

### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="В примере показан шаблон сцены на рабочем столе." border="false":::

## <a name="toolbar"></a>Панель инструментов

Панель инструментов — это контейнер для группировки набора элементов управления.

### <a name="top-use-cases"></a>Верхние случаи использования

* Контекстные действия в контенте приложения
* Контекстный фильтр и поиск
* Навигация и сухари

### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/ui-templates/mobile-toolbar.png" alt-text="В примере показан шаблон панели инструментов на мобильных устройствах." border="false":::

### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="В примере показан шаблон панели инструментов на рабочем столе." border="false":::
