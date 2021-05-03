---
title: Устранение проблем с отправкой в магазин
description: Понимание устранения неполадок и устранения проблем с отправкой Microsoft Teams магазина.
ms.topic: how-to
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 847534c68d013566e4bfbe0e5a1bbbe92e36e63e
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101910"
---
# <a name="resolve-issues-if-your-microsoft-teams-store-submission-fails"></a>Устранение проблем при сбойе Microsoft Teams хранения

Приложения, опубликованные в Microsoft Teams магазине, [](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) должны соответствовать рекомендациям по проверке Teams магазина и [политикам коммерческого рынка.](https://docs.microsoft.com/legal/marketplace/certification-policies)

Если отправка в магазине не выполняется, корпорация Майкрософт предоставляет службу проверки консьержа, которая поможет получить соответствие приложения и опубликовать его.

## <a name="get-help-directly-from-microsoft"></a>Получите помощь напрямую от Корпорации Майкрософт

Служба проверки консьержа, предоставляемая Корпорацией Майкрософт, помогает разработчикам публиковать свои приложения в Teams магазине. В рамках этой службы Корпорация Майкрософт проверяет, работает ли ваше приложение так, как описано, содержит все соответствующие метаданные и предоставляет пользователям значение.

В случае сбой отправки приложения Корпорация Майкрософт отправляет вам отчет о проверке с рекомендациями в течение 24 часов после отправки.

## <a name="resolve-issues-and-resubmit-your-app"></a>Устранение проблем и повторное

Перед повторной проверкой приложения в Центре партнеров необходимо устранить все проблемы, о чем сообщает группа проверки консьержей Майкрософт. Отчет Корпорации Майкрософт содержит следующие сведения:

* Соответствующее [руководство по проверке](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) для каждой проблемы
* Инструкции по воспроизведению каждой проблемы
* Рекомендации для решения каждой проблемы на основе общедоступных документов разработчика

Процесс решения проблем и повторной выдачи приложения обычно проходит так:

1. Вы устраняли все проблемы в отчете.
1. Вы отправляете следующее в команду проверки консьержа Майкрософт по <a href="mailto:teamsubm@microsoft.com">teamsubm@microsoft.com:</a>
   * Обновленный пакет приложений
   * Тестовые заметки для приложения (если они не были включены в исходное представление):
      * Учетные данные по крайней мере для двух учетных записей (один администратор и один не-администратор)
      * Инструкции по настройке приложения и проверке его функциональности
      * Видео, показывающая приложение, используемую в Teams
1. Группа проверки консьержа Майкрософт полностью тестирует обновленное приложение.
1. Вы делаете одно из следующих:
   * Если у приложения нет проблем, переограничите приложение в Центре партнеров.
   * Если проблемы не устранены или Корпорация Майкрософт находит новые проблемы, вы получите еще один отчет о том, что нужно исправить. Устранение этих проблем и отправка обновленной версии <a href="mailto:teamsubm@microsoft.com">приложения</a>в teamsubm@microsoft.com .

> [!CAUTION]
> Чтобы избежать нескольких сбоев в отправке, не переподавляйте приложение в Центре партнеров, пока команда проверки консьержа Майкрософт не утвердит ваше приложение.

## <a name="faq"></a>Вопросы и ответы

Получите ответы на некоторые распространенные вопросы при решении проблем с отправкой приложений.

<br>

<details>

<summary><b>Сколько времени займет публикация приложения?</b></summary>

Если у отправки в магазине нет проблем, ваше приложение будет публиковаться в течение 1-2 бизнес-дней. Если ваше приложение не работает, команда из Корпорации Майкрософт предоставляет вам рекомендации по устранению проблем. После исправления этих исправлений и повторной публикации обновленного приложения в эту команду вы будете уведомлены через 24 часа, если ваше приложение готово к публикации или по-прежнему нуждается в дополнительных работах.

<br>

</details>

<details>

<summary><b>Как повысить вероятность того, что мое приложение пройдет отправку?</b></summary>

Это может привести к успешной отправке:

1. Разработка приложения на основе рекомендаций [Teams разработки.](~/concepts/design/design-teams-app-overview.md)
1. Убедитесь, что ваше [приложение](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) придерживается рекомендаций по проверке Teams магазина и политики сертификации на коммерческом рынке [Майкрософт.](https://docs.microsoft.com/legal/marketplace/certification-policies)
1. Проверьте пакет приложения с помощью [Microsoft Teams проверки приложения.](https://dev.teams.microsoft.com/appvalidation.html)
1. [Подготовка отправки Teams магазина](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md).

<br>

</details>

<details>

<summary><b>Мое приложение находится в бета-тестировании. Могу ли я отправить свое приложение в любом случае, чтобы сэкономить время на процессе публикации?</b></summary>

Нет. Корпорация Майкрософт проверяет только готовые к производству приложения.

<br>

</details>

<details>

<summary><b>Могу ли я связаться с teamsubm@microsoft.com электронной почты перед первой отправкой приложения в Центре партнеров?</b></summary>

Нет. Корпорация Майкрософт не начинает проверку вашего приложения до тех пор, пока вы не представите приложение в Центре партнеров впервые.

<br>

</details>

<details>

<summary><b>Я получил сообщение из Центра партнеров о том, что мое приложение утверждено для публикации. Почему мое приложение не в Teams магазине?</b></summary>

После утверждения приложения публикация обычно занимает 1-2 бизнес-дня в зависимости от возможностей приложения.Если ваше приложение не опубликовано после двух дней работы, свяжитесь <a href="mailto:teamsubm@microsoft.com">с teamsubm@microsoft.com</a>.

<br>

</details>