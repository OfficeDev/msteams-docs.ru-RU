---
title: Разработка адаптивных карт для приложения
description: Узнайте, как создать адаптивные карты для Teams и получить Microsoft Teams пользовательского интерфейса.
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: b4d5f43268c7bd5afecb56d26eb0d49ed6c9002b
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630313"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a>Разработка адаптивных карт для Microsoft Teams приложения

Адаптивная карта содержит свободный набор элементов карт и необязательный набор действий. Адаптивные карты — это фрагменты контента, которые можно добавить в беседу с помощью бота или расширения обмена сообщениями. С помощью текстовых, графических и кнопок эти карточки обеспечивают насыщенную связь для вашей аудитории.

База адаптивной карты используется во многих продуктах Майкрософт, включая Teams. Вы можете отправлять карточки внутри сообщений пользователям с помощью ботов или расширений обмена сообщениями. Пользователи также могут принимать меры на картах при их настоящем действии.

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="Пример адаптивной карты." border="false":::

## <a name="microsoft-teams-ui-kit"></a>Комплект разработчика для пользовательского интерфейса Microsoft Teams

Дополнительные рекомендации по разработке адаптивных карт можно найти в Teams, включая элементы, которые можно захватить и изменить по мере необходимости, в Microsoft Teams пользовательского интерфейса. Набор пользовательского интерфейса также охватывает такие важные темы, как темы, доступность и размер отзывчивости.

> [!div class="nextstepaction"]
> [Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a>Конструктор адаптивных карт

Вы также можете приступить к разработке адаптивных карт непосредственно в браузере.

> [!div class="nextstepaction"]
> [Попробуйте конструктор адаптивных карт](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a>Типы адаптивных карт

### <a name="hero"></a>Главный имиджевый баннер

Наша самая большая карта. Используйте для общего доступа к статьям или сценариям, в которых изображение рассказывает большую часть истории.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="В примере показана карта героя адаптивной карты." border="false":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-hero-card.png" alt-text="В примере показана карта героя адаптивной карты на мобильных устройствах." border="false":::

---

### <a name="thumbnail"></a>Эскиз

Используйте для отправки простого действия сообщения.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="В примере показана карта адаптивной карты." border="false":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-thumbnail-card.png" alt-text="В примере показана карта адаптивных карт на мобильных устройствах." border="false":::

---

### <a name="list"></a>List

Используйте в сценариях, в которых пользователь должен выбрать элемент из списка, но для этих элементов не требуется много объяснений.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="В примере показана карта списка адаптивной карты." border="false":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-list-card.png" alt-text="В примере показана карта списка адаптивных карт на мобильном телефоне." border="false":::

---

### Digest

Use for news digests and round-up posts. Note: We recommend the thumbnail card for a single update or news item.

# [Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="Example shows an Adaptive Card digest card." border="false":::

# [Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-digest-card.png" alt-text="Example shows an Adaptive Card digest card on mobile." border="false":::

---

### <a name="media"></a>Мультимедиа

Используйте, когда нужно сочетать текст и носители, например аудио или видео.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="В примере показана медиакарда Adaptive Card." border="false":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-media-card.png" alt-text="В примере показана медиакарда Adaptive Card на мобильном телефоне." border="false":::

---

### <a name="people"></a>Люди

Лучше всего использовать для эффективного передачи данных о том, кто участвует в работе с задачей.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="В примере показана карточка людей адаптивной карты." border="false":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-people-card.png" alt-text="В примере показана карточка людей адаптивной карты на мобильных устройствах." border="false":::

---

### <a name="request-ticket"></a>Запрос билета

Используйте для получения быстрых входных данных от пользователя, чтобы автоматически создать задачу или билет.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="В примере показана карточка запроса на адаптивную карту." border="false":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-request-ticket-card.png" alt-text="В примере показана карточка для запроса билетов адаптивной карты на мобильный телефон." border="false":::

---

### <a name="image-set"></a>Набор изображений

Используйте для отправки нескольких эскизов изображений.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="В примере показана карта набора изображений адаптивной карты." border="false":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-image-set-card.png" alt-text="В примере показана карта набора изображений адаптивной карты на мобильных устройствах." border="false":::

---

### <a name="action-set"></a>Набор действий

Используйте для выбора кнопки пользователю, а затем соберем дополнительный ввод пользователя с той же карты.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="В примере показана карта набора действий адаптивной карты." border="false":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-action-set-card.png" alt-text="В примере показана карта набора действий адаптивной карты на мобильном телефоне." border="false":::

---

### <a name="choice-set"></a>Набор выбора

Используйте для сбора нескольких входных данных от пользователя.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="В примере показана карта выбора адаптивной карты." border="false":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-choice-set-card.png" alt-text="В примере показана карта выбора адаптивной карты на мобильном телефоне." border="false":::

---

## <a name="anatomy"></a>Анатомия

Адаптивные карты имеют большую гибкость. Но как минимум мы настоятельно рекомендуем включить следующие компоненты в каждую карту.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="В EExample показана анатомия адаптивной карты." border="false":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-anatomy.png" alt-text="В примере показана анатомия адаптивной карты на мобильных устройствах." border="false":::

---

|Счетчик|Описание|
|----------|-----------|
|A|**Заглавка.** Сделайте заготки четкими и краткими.|
|B|**Копия тела.** Передай сведения, которые слишком длинные или недостаточно важные, чтобы включить в заголовник.|
|C|**Основные** действия. В качестве наилучшей практики включаем 1-3 основных действия. Вы можете иметь до шести.|

## <a name="best-practices"></a>Рекомендации

Используйте эти рекомендации для создания качественного приложения.

### <a name="primary-and-secondary-actions"></a>Первичные и вторичные действия

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="Передовая практика по включению в адаптивную карту только небольшого набора действий." border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a>Do: Используйте до шести основных действий

Хотя адаптивные карты могут поддерживать шесть основных действий, большинству карт это не нужно. Действия должны быть четкими, краткими и прямыми. Меньше больше.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="Лучшая практика о том, как не перегружать пользователей слишком большим количеством действий на адаптивной карте." border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a>Не используйте более шести основных действий

Адаптивные карты должны представлять быстрое и оперативное содержимое. Слишком много действий может переполохить пользователя.

   :::column-end:::
:::row-end:::

### <a name="frequency"></a>Частота

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="Лучшая практика по частоте адаптивной карты." border="false":::

#### <a name="do-be-concise"></a>Do: Быть кратким

Можно легко отправить несколько карт в беседу, но после того, как карты прокрутки из виду, они становятся менее полезными. Попробуйте ограничиться основными. Это особенно актуально в канале, где пользователи менее терпимо воспринимают то, что они воспринимают как "шум".
