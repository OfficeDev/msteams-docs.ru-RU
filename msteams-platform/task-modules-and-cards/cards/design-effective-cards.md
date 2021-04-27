---
title: Разработка адаптивных карт для приложения
description: Узнайте, как создать адаптивные карты для teams и получить набор пользовательского интерфейса Microsoft Teams.
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 67a2882a0a687d5ccb48759419ecefcdf9396fc3
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020284"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a>Разработка адаптивных карт для приложения Microsoft Teams

Адаптивная карта содержит свободный набор элементов карт и необязательный набор действий. Адаптивные карты — это фрагменты контента, которые можно добавить в беседу с помощью бота или расширения обмена сообщениями. С помощью текстовых, графических и кнопок эти карточки обеспечивают насыщенную связь для вашей аудитории.

База адаптивной карты используется во многих продуктах Майкрософт, включая Teams. Вы можете отправлять карточки внутри сообщений пользователям с помощью ботов или расширений обмена сообщениями. Пользователи могут принимать меры на картах при их настоящем действии.

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="В примере показана адаптивная карта." border="false":::

## <a name="microsoft-teams-ui-kit"></a>Комплект разработчика для пользовательского интерфейса Microsoft Teams

Дополнительные рекомендации по разработке адаптивных карт в Teams, включая элементы, которые можно захватить и изменить по мере необходимости, можно найти в наборе пользовательского интерфейса Microsoft Teams. Набор пользовательского интерфейса также охватывает такие важные темы, как темы, доступность и размер отзывчивости.

> [!div class="nextstepaction"]
> [Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a>Конструктор адаптивных карт

Вы также можете приступить к разработке адаптивных карт непосредственно в браузере.

> [!div class="nextstepaction"]
> [Попробуйте конструктор адаптивных карт](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a>Типы адаптивных карт

### <a name="hero"></a>Главный имиджевый баннер

Наша самая большая карта. Используйте для общего доступа к статьям или сценариям, в которых изображение рассказывает большую часть истории.

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="В примере показана адаптивная карта." border="false":::

### <a name="thumbnail"></a>Эскиз

Используйте для отправки простого действия сообщения.

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="Пример адаптивной карты." border="false":::

### <a name="list"></a>List

Используйте в сценариях, в которых пользователь должен выбрать элемент из списка, но для этих элементов не требуется много объяснений.

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="Пример адаптивной карты." border="false":::

### <a name="digest"></a>Digest

Используйте для дайджестов новостей и публикаций обнаглеть. Примечание. Рекомендуется использовать карту эскиза для одного обновления или элемента новостей.

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="На рисунке показана адаптивная карта." border="false":::

### <a name="media"></a>Мультимедиа

Используйте, когда нужно сочетать текст и носители, например аудио или видео.

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="На рисунке показана адаптивная карта." border="false":::

### <a name="people"></a>Люди

Лучше всего использовать для эффективного передачи данных о том, кто участвует в работе с задачей.

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="Иллюстрация адаптивной карты." border="false":::

### <a name="request-ticket"></a>Запрос билета

Используйте для получения быстрых входных данных от пользователя, чтобы автоматически создать задачу или билет.

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="Иллюстрация адаптивной карты." border="false":::

### <a name="imageset"></a>ImageSet

Используйте для отправки нескольких эскизов изображений.

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="Пример адаптивной карты." border="false":::

### <a name="actionset"></a>ActionSet

Используйте для выбора кнопки пользователю, а затем соберем дополнительный ввод пользователя с той же карты.

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="В примере показана адаптивная карта." border="false":::

### <a name="choiceset"></a>ChoiceSet

Используйте для сбора нескольких входных данных от пользователя.

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="В примере отображается адаптивная карта." border="false":::

## <a name="anatomy"></a>Анатомия

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="Иллюстрация, показывающая анатомию пользовательского интерфейса адаптивной карты." border="false":::

Адаптивные карты имеют большую гибкость. Но как минимум мы настоятельно рекомендуем включить в каждую карту следующие компоненты:

|Счетчик|Описание|
|----------|-----------|
|A|**Заглавная:** Сделать заглавные заготки четкими и краткими, но описательными.|
|B|**Копия тела.** Используйте для передачи слишком длинных или недостаточно важных деталей для включаемой в заголовок.|
|C|**Основные** действия. В качестве наилучшей практики включаем 1-3 основных действия. Разрешено не более шести.|

## <a name="best-practices"></a>Рекомендации

### <a name="primary-and-secondary-actions"></a>Первичные и вторичные действия

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="Пример наилучшей практики адаптивных карт." border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a>Do: Используйте до шести основных действий

Хотя адаптивные карты могут поддерживать шесть основных действий, большинству карт это не нужно. Действия должны быть четкими, краткими и прямыми. Меньше больше.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="В примере показана лучшая практика адаптивных карт." border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a>Не используйте более шести основных действий

Адаптивные карты должны представлять быстрое и оперативное содержимое. Слишком много действий может переполохить пользователя.

   :::column-end:::
:::row-end:::

### <a name="frequency"></a>Частота

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="Иллюстрация с лучшими примерами адаптивных карт." border="false":::

#### <a name="do-be-concise"></a>Do: Быть кратким

Можно легко отправить несколько карт в беседу, но после того, как карты прокрутки из виду, они становятся менее полезными. Попробуйте ограничиться основными. Это особенно актуально в канале, где пользователи менее терпимо воспринимают то, что они воспринимают как "шум".
