---
title: Проектирование уведомлений ленты новостей
author: heath-hamilton
description: Узнайте, как спроектировать уведомления веб-канала действий для приложения Teams и получить комплект пользовательского интерфейса Teams. Разработка уведомлений из канала Teams в Visual Studio C#
ms.localizationpriority: medium
ms.author: surbhigupta
ms.topic: reference
ms.openlocfilehash: 9a17027f7dd68993a118f24bb23cfff0a56651e1
ms.sourcegitcommit: 4ba6392eced76ba6baeb6d6dd9ba426ebf4ab24f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/21/2022
ms.locfileid: "66919769"
---
# <a name="designing-activity-feed-notifications-for-your-microsoft-teams-app"></a>Проектирование уведомлений веб-канала действий для приложения Microsoft Teams

Веб-канал действий — это область для доступа пользователей к уведомлениям в Microsoft Teams. Веб-канал сохраняет уведомления за последние четыре недели.

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/activity-feed/mobile-overview.png" alt-text="В примере показано уведомление приложения, отображаемое в веб-канале действий Teams на мобильных устройствах.":::

# <a name="desktop"></a>[Компьютер](#tab/desktop)

:::image type="content" source="../../assets/images/activity-feed/desktop-overview.png" alt-text="В примере показано уведомление приложения, отображаемое в веб-канале действий Teams.":::

---

## <a name="anatomy"></a>Структура

:::image type="content" source="../../assets/images/activity-feed/activity-feed-card-anatomy.png" alt-text="Структура структуры уведомления веб-канала действий Teams.":::

|Счетчик|Описание|
|----------|-----------|
|1|**Аватар**: показывает, кто инициировал действие.|
|2|**Тип действия или значок приложения**: отображает тип действия. Для уведомлений приложения значок строки заменяется значком приложения.|
|3|**Заголовок (первая строка): Actor + reason**: *Actor: Name* of the user or app that initiated the activity. *Причина*. Описывает действие.|
|4|**Метка времени**: показывает, когда произошло действие.|
|5|**Расположение (вторая строка)**: показывает, где произошло действие в Teams.|
|6|**Предварительный просмотр текста (третья строка)**: отображает усеченную строку с начала уведомления.|

## <a name="types-of-activity-feed-notification-cards"></a>Типы карт уведомлений веб-канала действий

В следующих вариантах показаны типы карт уведомлений веб-канала действий, которые можно отобразить. Логотип приложения заменяет аватар пользователя для уведомлений, созданных приложением.

:::image type="content" source="../../assets/images/activity-feed/activity-feed-card-types.png" alt-text="Варианты карточек веб-каналов действий Teams.":::

## <a name="manage-activity-feed-notifications"></a>Управление уведомлениями веб-канала действий

Пользователи могут управлять уведомлениями, отправленными из вашего приложения, на странице параметров Teams.

## <a name="related-system-notifications"></a>Связанные системные уведомления

Каждое действие создает системное уведомление. Отображаемые данные зависят от настроек пользователя в параметрах уведомлений. Пользователи также могут выбрать стиль уведомлений в зависимости от операционной системы.

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/activity-feed/mobile-related-system-notifications.png" alt-text="Варианты карточек веб-каналов действий Teams в Android и iOS.":::

|Счетчик|Описание|
|----------|-----------|
|1|Android|
|2|iOS|

# <a name="desktop"></a>[Компьютер](#tab/desktop)

:::image type="content" source="../../assets/images/activity-feed/related-system-notifications.png" alt-text="Варианты карт действий Teams в разных операционных системах.":::

|Счетчик|Описание|
|----------|-----------|
|1|Настраиваемое приложение Teams|
|2|Windows|
|3|Mac|

---

## <a name="step-by-step-guide"></a>Пошаговые инструкции

Следуйте [пошаговое руководство по](../../sbs-graphactivity-feedbroadcast.yml) отправке уведомлений веб-канала действий в Teams.

## <a name="next-step"></a>Следующее действие

> [!div class="nextstepaction"]
> [Реализация уведомлений веб-канала действий](/graph/teams-send-activityfeednotifications)
