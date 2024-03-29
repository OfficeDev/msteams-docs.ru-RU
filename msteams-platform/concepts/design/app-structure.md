---
title: Разработайте приложение — познакомьтесь с его структурой
description: В этом модуле вы узнаете, что можно и не можете настроить в Microsoft Teams при разработке структуры приложения.
author: heath-hamilton
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: surbhigupta
ms.openlocfilehash: 6a409accc5f55aa0a9c245aa061efde5b67d81f3
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558760"
---
# <a name="understand-the-microsoft-teams-app-structure"></a>Понимание структуры приложений Microsoft Teams

При создании приложения важно знать, что можно и что нельзя настраивать в Microsoft Teams. Эти сведения могут помочь лучше понять, какие части приложения контролируемы.

Следующие вайрфреймы показывают:

* Поверхности, которые можно настроить в каждой возможности приложения Teams (обведены розовым цветом).
* Области, поддерживаемые каждой возможностью.

> [!TIP]
> **Что значит область?** Область — это пространство в Teams, где люди могут использовать приложение. Приложения могут иметь одну или несколько областей, включая личную область, каналы, чаты и собрания.

## <a name="personal-apps"></a>Персональные приложения

Персональные приложения предоставляют большой холст для размещения содержимого приложения для отдельных пользователей.

***Поддерживаемые области:**: Личные*

### <a name="mobile"></a>Мобильная версия

Холст представляет собой веб-просмотр, поэтому вы можете полностью настроить работу.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-mobile.png" alt-text="Концептуальное изображение, показывающее интерфейсные области в Teams, которые разработчики могут настраивать для личных приложений на мобильных устройствах.":::

### <a name="desktop"></a>Версия для настольного компьютера

Холст — это iframe, позволяющий полностью настроить работу.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-desktop.png" alt-text="Концептуальное изображение, показывающее интерфейсные области в Teams, которые разработчики могут настраивать для личных приложений на настольном компьютере.":::

## <a name="tabs"></a>Вкладки

Вкладки предоставляют большой холст для размещения содержимого приложения для группы пользователей. Можно включать вкладки в общие пространства, такие как каналы, чаты и приглашения на собрания.

***Поддерживаемые области**: каналы, чаты, собрания*

### <a name="mobile"></a>Мобильная версия

Холст представляет собой веб-просмотр, поэтому вы можете полностью настроить работу.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-mobile.png" alt-text="Концептуальное изображение, показывающее интерфейсные области в Teams, которые разработчики могут настраивать для вкладок на мобильных устройствах.":::

### <a name="desktop"></a>Версия для настольного компьютера

Холст — это iframe, позволяющий полностью настроить работу.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-desktop.png" alt-text="Концептуальное изображение, показывающее интерфейсные области в Teams, которые разработчики могут настраивать для вкладок на рабочем столе.":::

## <a name="bots"></a>боты;

Боты — это диалоговые приложения, которые интегрируются со встроенными функциями обмена сообщениями Teams, поэтому работа с пользовательским интерфейсом выполняется за вас. С точки зрения дизайна, все еще есть возможности для добавления индивидуальности, пользовательских функций и богатых, полезных сведений с нашей поддержкой обработки естественной речи (NLP) и платформой Adaptive Cards.

***Поддерживаемые области**: Личные, Каналы, Чаты, Собрания*

### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-mobile.png" alt-text="Концептуальное изображение, показывающее интерфейсные области в Teams, которые разработчики могут настраивать для ботов на мобильных устройствах.":::

### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-desktop.png" alt-text="Концептуальное изображение, показывающее интерфейсные области в Teams, которые разработчики могут настраивать для ботов на рабочем столе.":::

## <a name="message-extensions"></a>Расширения для сообщений

Расширения для обмена сообщениями — это ярлыки для вставки содержимого приложения или действий с сообщением без выхода из беседы. Расширения сообщений на основе действий дают вам больший контроль над взаимодействием, в то время как Teams обрабатывает большую часть того, что отображается для расширений сообщений на основе поиска.

***Поддерживаемые области**: Личные, Каналы, Чаты, Собрания*

### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-mobile.png" alt-text="Концептуальное изображение, показывающее интерфейсные области в Teams, которые разработчики могут настраивать для расширений сообщений на мобильных устройствах.":::

### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-desktop.png" alt-text="Концептуальное изображение, показывающее интерфейсные области в Teams, которые разработчики могут настраивать для расширений сообщений на рабочем столе.":::

## <a name="meeting-extensions"></a>Расширения для собраний

Расширения собраний — это приложения для улучшения прямых собраний. Вы можете размещать содержимое своего приложения в нескольких сценариях, в том числе до, во время и после собраний.

***Поддерживаемые области**: встречи, чаты*

### <a name="mobile"></a>Мобильная версия

Поверхность представляет собой веб-просмотр, позволяющий настраивать работу, но имейте в виду, что во время собраний эти приложения используют темную тему.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-mobile.png" alt-text="Концептуальное изображение, показывающее интерфейсные области в Teams, которые разработчики могут настраивать для расширений собраний на мобильных устройствах.":::

### <a name="desktop"></a>Версия для настольного компьютера

Поверхность — это iframe, что позволяет настраивать работу, но имейте в виду, что во время собраний эти приложения используют темную тему и тесноваты.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-desktop.png" alt-text="Концептуальное изображение, показывающее интерфейсные области в Teams, которые разработчики могут настраивать для расширений собраний на рабочем столе.":::
