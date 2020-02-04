---
title: Справочные материалы по проектированию
description: Описывает рекомендации по использованию диалоговых окон в приложениях
keywords: рекомендации по проектированию Teams Справочник по компонентам
ms.openlocfilehash: d244eedde66085d41b1f356176a7775de304aaf4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675245"
---
# <a name="dialogs"></a>Диалоги

Диалоговые окна следует использовать экономно, так как они могут нарушить работу, и у пользователя должен быть очевидный способ выхода.

---

## <a name="sizes"></a>Масштаба

У нас есть 3 варианта размеров диалоговых окон. Выберите размер, который подходит для имеющегося содержимого.
[!include[Dialog sizes](~/includes/design/dialogs-image-sizes.html)]

---

## <a name="buttons"></a>Кнопки

Кнопки выравниваются по правому краю.
Все остальные элементы (флажки, текст справки и т. д.) должны быть выровнены по левому краю.
Не повторяйте отрицательные действия (никогда не предоставляйте кнопку ' X ' и ' Cancel ' одновременно).
Кнопки "Применить" должны быть связаны с кнопками "Отмена".
[!include[Dialog buttons](~/includes/design/dialogs-image-buttons.html)]

---

## <a name="scrolling"></a>Прокрутки

В некоторых случаях содержимое будет прокручено. Заголовок диалогового окна и другие важные сведения остаются на месте.
[!include[Dialog scrolling](~/includes/design/dialogs-image-scrolling.html)]

---

## <a name="padding"></a>Внутренние поля

Заполнение всеми четырьмя сторонами диалогового окна должно быть интервалами по 32.
[!include[Dialog padding](~/includes/design/dialogs-image-padding.html)]

---

## <a name="typography"></a>Шрифтовое оформление

Мы используем Семиболд UI в 18pt (title2) и $app-Black для заголовков диалоговых окон. Для основного текста мы используем регулярный пользовательский интерфейс в 14pt (Base) и $app-Black.
[!include[Dialog typography](~/includes/design/dialogs-image-typography.html)]