---
title: Общий доступ к кнопке Teams Embedded
description: Добавление на веб-сайт кнопки "общий доступ" для Teams
keywords: Совместное использование Teams в Teams
ms.openlocfilehash: 219724e6ef3448db8a5b1fc70a519803255ffee6
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675515"
---
# <a name="creating-a-share-to-teams-embedded-button"></a>Создание общего доступа к кнопке Teams Embedded

>[!NOTE]
> * Поддерживаются только настольные версии Edge и Chrome.
> * Использование учетных записей Фримиум или Guest не поддерживается.

Сторонние веб-сайты могут использовать сценарий запуска для встраивания общего доступа к кнопкам Teams на своих веб-страницах, которые запустят общий доступ к Microsoft Teams во всплывающем окне при нажатии. Это позволит предоставить ссылку непосредственно любому человеку или каналу Microsoft Teams без переключения контекста.

![Открыть доступ к всплывающему меню "команды"](~/assets/images/share-to-teams-popup.png)

## <a name="how-to-embed-a-share-to-teams-button"></a>Как внедрить кнопку Share to Teams

Сначала необходимо добавить `launcher.js` скрипт на веб-страницу.

```html
<script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
```

Затем добавьте HTML-элемент на веб-страницу с атрибутом `teams-share-button` Class и ссылка для совместного использования в `data-href` атрибуте.

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>">
</div>
```

При этом значок Microsoft Teams будет добавлен на веб-сайт.

![Значок предоставления общего доступа к Teams](~/assets/icons/share-to-teams-icon.png)

При необходимости используйте `data-icon-px-size` атрибут, если вы хотите изменить размер значков для кнопки Общий доступ для групп.

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-icon-px-size="64">
</div>
```

Если вы знаете, что предварительный просмотр URL-адреса с вашей ссылки на общий доступ не отображается в Teams (например, для ссылки требуется проверка подлинности пользователя), можно отключить `data-preview` предварительный просмотр `false`URL-адреса, добавив атрибут в значение.

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-preview="false">
</div>
```

Если страница динамически отрисовывает содержимое, можно использовать метод, `shareToMicrosoftTeams.renderButtons()` чтобы принудительно отобразить кнопку " **общий доступ** " для соответствующего места в конвейере.

## <a name="crafting-your-website-preview"></a>Создание предварительной версии веб-сайта

Когда ваш веб-сайт совместно используется в Teams, карточка, вставленная в выбранный канал, будет содержать предварительный просмотр веб-сайта. Вы можете управлять поведением этого предварительного просмотра, убедившись, что соответствующие метаданные добавляются на веб-сайт, к которому предоставлен `data-href` общий доступ (URL-адрес). В таблице ниже представлены необходимые теги. Можно использовать либо версии HTML по умолчанию, либо открытую версию графика.

Для отображения предварительного просмотра необходимо выполнить следующие действия:

* Включите либо эскиз, либо заголовок и описание (для достижения лучших результатов, включая все три).
* URL-адрес, к которому предоставлен общий доступ, не может требовать аутентификации. Если вы по-прежнему можете поделиться им, но Предварительная версия не будет создана.

|Значение|Метатег| Открытие графика|
|----|----|----|
|Название|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|Описание|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|Изображение эскиза| нет |`<meta property="og:image" content="http://example.com/image.jpg">`|

## <a name="share-to-teams-for-education"></a>Совместный доступ к Microsoft Teams для образовательных учреждений

Для преподавателей, использующих кнопку Share to Teams, вы получите дополнительные возможности `Create an Assignment`. Это позволяет быстро создать назначение в выбранной группе на основе общей ссылки.

![Открыть доступ к всплывающему меню "команды"](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a>Определение полного загрузчика. js

| Свойство | Атрибут HTML | Тип | По умолчанию | Описание |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| href | `data-href` | строка | н/д | Значение href для общего доступа к контенту. |
| preview | `data-preview` | Логическое значение (в виде строки) | `true` | Указывает, следует ли отображать содержимое для совместного использования. |
| иконпкссизе | `data-icon-px-size` | Number (как строка) | `32` | Размер в пикселях кнопки Share to Teams для отображения. |
| мсгтекст | `data-msg-text` | строка | н/д | Текст по умолчанию, вставляемый перед ссылкой в поле создания сообщения (предельное число знаков в 200) |
| ассигнинстр | `data-assign-instr` | строка | н/д | Текст по умолчанию, вставляемый в поле "инструкции" для назначений (количество знаков в 200) |
| ассигнтитле | `data-assign-title` | строка | н/д | Текст по умолчанию, вставляемый в поле "название" для назначений (50 знаков) |

### <a name="methods"></a>Методы

**`shareToMicrosoftTeams.renderButtons(options)`**

`options`(необязательно):`{ elements?: HTMLElement[] }`

Отображает все кнопки общего доступа на странице. Если необязательный `options` объект предоставляется со списком элементов, эти элементы отображаются на кнопках совместного использования.

### <a name="setting-default-form-values"></a>Установка значений формы по умолчанию

При необходимости можно задать значения по умолчанию для следующих полей в форме Share to teams:

* Произнесите что-то`msgText`вроде this ().
* Инструкции по назначению (`assignInstr`)
* Название назначения (`assignTitle`)

#### <a name="example-default-form-values"></a>Пример: значения формы по умолчанию

```html
<span
    class="teams-share-button"
    data-href="https://www.microsoft.com/education/products/teams"
    data-msg-text="Default Message"
    data-assign-title="Default Assignment Title"
    data-assign-instr="Default Assignment Instructions"
></span>
```
