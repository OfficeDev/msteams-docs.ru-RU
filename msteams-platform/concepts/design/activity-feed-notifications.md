---
title: Проектирование уведомлений каналов активности
author: heath-hamilton
description: Узнайте, как создать уведомления о канале активности для Teams приложения и получить Microsoft Teams пользовательского интерфейса.
ms.localizationpriority: medium
ms.author: surbhigupta
ms.topic: reference
ms.openlocfilehash: 552541e17422d20297d857a4273ec807d11e6928
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157528"
---
# <a name="designing-activity-feed-notifications-for-your-microsoft-teams-app"></a>Проектирование уведомлений каналов активности для Microsoft Teams приложения

Канал действий — это поверхность для доступа пользователей к уведомлениям в Microsoft Teams. Канал сохраняет уведомления за последние четыре недели.

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/activity-feed/mobile-overview.png" alt-text="В примере показано уведомление приложения, отображаемое в Teams канале активности на мобильном телефоне." border="false":::

# <a name="desktop"></a>[Компьютер](#tab/desktop)

:::image type="content" source="../../assets/images/activity-feed/desktop-overview.png" alt-text="В примере отображается уведомление приложения, отображаемая в Teams канале действий." border="false":::

---

## <a name="anatomy"></a>Структура

:::image type="content" source="../../assets/images/activity-feed/activity-feed-card-anatomy.png" alt-text="Разработка анатомии уведомления Teams канала действий." border="false":::

|Счетчик|Описание|
|----------|-----------|
|1|**Аватар:** Показывает, кто инициировал действие.|
|2|**Значок типа действия и приложения:** описывает тип действия. Для уведомлений приложения значок строки заменяется значком приложения.|
|3|**Название (первая строка): Actor + reason**: *Actor*: Name of the user or app that initiated the activity. *Причина.* Описывает действие.|
|4 |**Timestamp**: Показывает, когда действие произошло.|
|5 |**Расположение (вторая строка)**: показывает, где происходило действие в Teams.|
|6 |**Tertiary information (third line)**: Optional. Показывает предварительный текст или дополнительные сведения.|

## <a name="types-of-activity-feed-notification-cards"></a>Типы карт уведомлений о канале активности

В следующих вариантах отображаются типы карт уведомлений о канале активности. Логотип приложения заменяет аватар пользователя для уведомлений, созданных приложениями.

:::image type="content" source="../../assets/images/activity-feed/activity-feed-card-types.png" alt-text="Варианты Teams ленты действий." border="false":::

## <a name="manage-activity-feed-notifications"></a>Управление уведомлениями о канале действий

Пользователи могут управлять уведомлениями, отправленные из приложения на Teams параметров.

## <a name="related-system-notifications"></a>Связанные системные уведомления

Каждое действие создает системные уведомления. Отображаемые данные зависят от настройки пользователя в параметрах уведомлений. Пользователи также могут выбрать стиль уведомлений на основе своей операционной системы.

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/activity-feed/mobile-related-system-notifications.png" alt-text="Варианты Teams на Android и iOS." border="false":::

|Счетчик|Описание|
|----------|-----------|
|1|Android|
|2|iOS|

# <a name="desktop"></a>[Компьютер](#tab/desktop)

:::image type="content" source="../../assets/images/activity-feed/related-system-notifications.png" alt-text="Варианты Teams на разных операционных системах." border="false":::

|Счетчик|Описание|
|----------|-----------|
|1|Teams настраиваемый|
|2|Windows|
|3|Mac|

---

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Реализация уведомлений о канале действий](/graph/teams-send-activityfeednotifications)
