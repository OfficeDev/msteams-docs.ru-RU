---
title: Разработка адаптивных карточек для приложения
description: Узнайте, как создать адаптивные карточки для Teams и получить комплект разработчика для пользовательского интерфейса Microsoft Teams.
localization_priority: Priority
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 28a6b794b9ebae88f8895013f945cbf3b4a91e87
ms.sourcegitcommit: 306b6e8cb3aac8bfda10ef3999467a797d64539d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/20/2021
ms.locfileid: "58408659"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a>Разработка адаптивных карточек для приложения Microsoft Teams

Адаптивная карточка содержит произвольный текст элементов карточки и необязательный набор действий. Адаптивные карточки — это фрагменты содержимого с действиями, которые можно добавить в беседу с помощью бота или расширения для сообщений. Эти карточки с помощью текста, графики и кнопок обеспечивают широкие возможности взаимодействия с аудиторией.

Инфраструктура адаптивных карточек используется во многих продуктах Майкрософт, включая Teams. Вы можете отправлять карточки внутри сообщений пользователям с помощью ботов или расширений для сообщений. Кроме того, пользователи могут выполнять действия в карточках при их просмотре.

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="Обзор примера адаптивной карточки." border="false":::

## <a name="microsoft-teams-ui-kit"></a>Комплект разработчика для пользовательского интерфейса Microsoft Teams

В комплекте разработчика для пользовательского интерфейса Microsoft Teams можно найти более полные рекомендации по проектированию адаптивных карточек в Teams, в том числе элементы, которые можно изменять по своему усмотрению. В комплекте разработчика для пользовательского интерфейса также охвачены такие важные области, как тема, специальные возможности и адаптивный размер.

> [!div class="nextstepaction"]
> [Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a>Конструктор адаптивных карточек

Вы также можете приступить к разработке адаптивных карточек непосредственно в браузере.

> [!div class="nextstepaction"]
> [Попробовать конструктор адаптивных карточек](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a>Типы адаптивных карточек

### <a name="hero"></a>Главный имиджевый баннер

Наша самая большая карточка. Используется для публикации статей или сценариев, в которых изображение играет важнейшую роль.

#### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/adaptive-cards/mobile-hero-card.png" alt-text="Пример адаптивной карточки главного имиджевого баннера на мобильном устройстве." border="false":::

#### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="Пример адаптивной карточки главного имиджевого баннера." border="false":::

### <a name="thumbnail"></a>Эскиз

Используется для отправки простого сообщения с действиями.

#### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/adaptive-cards/mobile-thumbnail-card.png" alt-text="Пример адаптивной карточки эскиза на мобильном устройстве." border="false":::

#### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="Пример адаптивной карточки эскиза." border="false":::

### <a name="list"></a>Список

Используется в сценариях, где пользователь должен выбирать элемент из списка, а элементам не требуется подробное объяснение.

#### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/adaptive-cards/mobile-list-card.png" alt-text="Пример адаптивной карточки списка на мобильном устройстве." border="false":::

#### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="Пример адаптивной карточки списка." border="false":::

### <a name="digest"></a>Дайджест

Используется для новостных дайджестов и сводных публикаций. Примечание. Рекомендуем использовать карточку эскиза для одного обновления или новости.

#### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/adaptive-cards/mobile-digest-card.png" alt-text="Пример адаптивной карточки дайджеста на мобильном устройстве." border="false":::

#### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="Пример адаптивной карточки дайджеста." border="false":::

### <a name="media"></a>Мультимедиа

Используется при объединении текста и мультимедиа, например звука или видео.

#### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/adaptive-cards/mobile-media-card.png" alt-text="Пример адаптивной карточки мультимедиа на мобильном устройстве." border="false":::

#### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="Пример адаптивной карточки мультимедиа." border="false":::

### <a name="people"></a>Люди

Лучше всего использовать для эффективного уведомления о тех, кто участвует в задаче.

#### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/adaptive-cards/mobile-people-card.png" alt-text="Пример адаптивной карточки людей на мобильном устройстве." border="false":::

#### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="Пример адаптивной карточки людей." border="false":::

### <a name="request-ticket"></a>Запрос

Используется для быстрого получения входных данных от пользователя с целью автоматического создания задачи или запроса.

#### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/adaptive-cards/mobile-request-ticket-card.png" alt-text="Пример адаптивной карточки запроса на мобильном устройстве." border="false":::

#### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="Пример адаптивной карточки запроса." border="false":::

### <a name="image-set"></a>Набор изображений

Используется для отправки нескольких эскизов изображений.

#### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/adaptive-cards/mobile-image-set-card.png" alt-text="Пример адаптивной карточки набора изображений на мобильном устройстве." border="false":::

#### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="Пример адаптивной карточки набора изображений." border="false":::

### <a name="action-set"></a>Набор действий

Используется, когда пользователю нужно нажимать кнопку с последующим сбором дополнительных входных данных пользователя с той же карточки.

#### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/adaptive-cards/mobile-action-set-card.png" alt-text="Пример адаптивной карточки набора действий на мобильном устройстве." border="false":::

#### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="Пример адаптивной карточки набора действий." border="false":::

### <a name="choice-set"></a>Набор вариантов

Используется для сбора нескольких входных данных от пользователя.

#### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/adaptive-cards/mobile-choice-set-card.png" alt-text="Пример адаптивной карточки набора вариантов на мобильном устройстве." border="false":::

#### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="Пример адаптивной карточки набора вариантов." border="false":::

## <a name="anatomy"></a>Структура

Адаптивные карточки обладают большой гибкостью. Но как минимум мы настоятельно рекомендуем включать следующие компоненты в каждую карточку.

#### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/adaptive-cards/mobile-anatomy.png" alt-text="Пример адаптивной карточки структуры на мобильном устройстве." border="false":::

|Счетчик|Описание|
|----------|-----------|
|A|**Заголовок**. Создавайте ясные и четкие заголовки.|
|Б|**Копия основного текста**. Сообщайте сведения, слишком длинные или недостаточно важные для включения в заголовок.|
|В|**Основные действия**. Рекомендуется включить от 1 до 3 основных действий. Вы можете выбрать до шести действий.|

#### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="Пример адаптивной карточки структуры." border="false":::

|Счетчик|Описание|
|----------|-----------|
|A|**Заголовок**. Создавайте ясные и четкие заголовки.|
|Б|**Копия основного текста**. Сообщайте сведения, слишком длинные или недостаточно важные для включения в заголовок.|
|В|**Основные действия**. Рекомендуется включить от 1 до 3 основных действий. Вы можете выбрать до шести действий.|

## <a name="best-practices"></a>Рекомендации

Используйте эти рекомендации для создания качественных приложений.

### <a name="primary-and-secondary-actions"></a>Основные и вспомогательные действия

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="Рекомендация о включении в адаптивную карточку только небольшого набора действий." border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a>Рекомендуется: используйте до шести основных действий

Адаптивные карточки могут поддерживать шесть основных действий, но большинству карточек это не требуется. Действия должны быть четкими, краткими и простыми. Чем меньше, тем лучше.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="Рекомендация о том, как не перегружать пользователей слишком большим количеством действий на адаптивной карточке." border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a>Не рекомендуется: используйте более шести основных действий

Адаптивные карточки должны представлять быстрое интерактивное содержимое. Слишком много действий могут перегружать пользователя.

   :::column-end:::
:::row-end:::

### <a name="frequency"></a>Частота

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="Рекомендация по частоте использования адаптивной карточки." border="false":::

#### <a name="do-be-concise"></a>Рекомендуется: будьте краткими

В беседу можно легко отправить несколько карточек, но после прокрутки и исчезновения карточек с экрана они становятся менее полезными. Попробуйте ограничиться основными моментами. Это особенно актуально в каналах, где пользователи более склонны воспринимать элементы как ненужный "шум".
