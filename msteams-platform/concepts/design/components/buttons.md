---
title: Справочные материалы по проектированию
description: Описывает рекомендации по использованию кнопок, ссылок и элементов управления в приложениях
keywords: рекомендации по разработке Teams ссылки на компоненты кнопки ссылки на цвета
ms.openlocfilehash: b9325980c38048ee250ace6b00f1ed29c6cbea8d
ms.sourcegitcommit: 61edf47c9dd1dbc1df03d0d9fb83bfedca4c423b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2020
ms.locfileid: "43914590"
---
# <a name="buttons-links-and-controls"></a>Кнопки, ссылки и элементы управления

---

## <a name="button-types"></a>Типы кнопок

Способ оформления кнопок позволяет сообщить, какие действия они вызывают. Мы поддерживаем широкий спектр кнопок, отформатированных для отображения различных уровней выделения.

У кнопок может быть текст, значок или комбинация текста и значок. Для связи разных уровней в иерархии мы разработали основные и дополнительные кнопки в каждой категории.

### <a name="fluent-design-system"></a>Система дизайна Fluent

Пользовательский интерфейс Fluent предоставляет рекомендации по состояниям веб-компонентов, стилей и специальных возможностей для веб-компонентов. Кнопки на платформе Teams можно отформатировать для отображения различных уровней выделения. В этом *разделе представлены*[цвета кнопок пользовательского интерфейса Fluent](https://fluentsite.z22.web.core.windows.net/components/button/definition?showCode=false&showRtl=false&showTransparent=false&showVariables=true#types-emphasis) для HTML и шестнадцатеричных значений CSS.  

### <a name="text-buttons"></a>Текстовые кнопки

В диалоговых окнах необходимо выровнять кнопки вправо, начиная с основного действия, расположенного справа. В карточках кнопки выравниваются по левому краю.

Стили кнопок в Teams

Клиент для настольных ПК[!include[Button states](~/includes/design/buttons-image-states.html)]

Мобильный клиент[!include[Mobile button states](~/includes/design/buttons-mobile-image-states.html)]

Кнопки диалоговых окон[!include[Dialog buttons](~/includes/design/buttons-image-dialog.html)]

Состояния кнопок карточки[!include[Card button states](~/includes/design/buttons-image-cardstates.html)]

Кнопки карточки[!include[Card buttons](~/includes/design/buttons-image-card.html)]

### <a name="icon-buttons"></a>Кнопки со значками

Кнопки значка могут вызывать действие, а также включать и отключать их.
[!include[Icon buttons](~/includes/design/buttons-image-icon.html)]

В некоторых случаях можно связать значок и текст, чтобы увеличить выделение.
[!include[Icon text buttons](~/includes/design/buttons-image-icontext.html)]

### <a name="miscellaneous-buttons"></a>Различные кнопки

#### <a name="desktop-clients"></a>Клиенты для настольных ПК
Радиальные кнопки, флажки и выключатели.<br/>
[!include[Other buttons](~/includes/design/buttons-image-others.html)]

#### <a name="mobile-clients"></a>Мобильные клиенты
Радиальные кнопки, флажки и выключатели.<br/>
[!include[Other buttons](~/includes/design/buttons-image-mobile-others.html)]

---

## <a name="links"></a>Links

Ниже приведены утвержденные стили для ссылок на внутренние текстовые ссылки.
[!include[Approved link styles](~/includes/design/links-image-text.html)]

---

## <a name="style"></a>Стиль

## <a name="size-and-padding"></a>Размер и заполнение

Текстовые кнопки, значки и элементы управления располагаются в высшем контейнере интервалами по 32, чтобы все элементы управления были визуально выровнены и согласованы.
[!include[Size and padding](~/includes/design/style-image-size.html)]

### <a name="rounded-corners"></a>Скругленные углы

Текстовые кнопки имеют угловой радиус 3 ПКС.
[!include[Rounded corners](~/includes/design/style-image-corners.html)]

### <a name="button-text"></a>Текст кнопки

Используйте регистр предложений в тексте для кнопок, чтобы упростить локализацию и разборчивость. (Другими словами, только первая буква первого слова в фразе или предложении заменяется на прописную.)
