---
title: Создание кнопки «Поделиться в Teams»
description: Добавление встроенной кнопки "Поделиться в Teams" на веб-сайте
ms.topic: reference
keywords: Совместное share-to-Teams Teams
ms.openlocfilehash: 46091c957137cc871095ca6a57c0d61fa79d9458
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014336"
---
# <a name="create-a-share-to-teams-button-for-your-website"></a>Создайте кнопку «Поделиться в Teams» для своего сайта

>[!NOTE]
> * Поддерживаются только классические версии Edge и Chrome.
> * Использование учетных записей Freemium или гостевых учетных записей не поддерживается.

Сторонние веб-сайты могут использовать сценарий запуска, чтобы встраить кнопки "Поделиться" в teams на своих веб-странице, что позволит при нажатии на них запускать окне "Поделиться в Teams" во всплывающее окно. Это позволит вам делиться ссылкой непосредственно с любым человеком или каналом Microsoft Teams без переключения контекста.

![Всплывающее всплывающее окна "Поделиться в Teams"](~/assets/images/share-to-teams-popup.png)

## <a name="how-to-embed-a-share-to-teams-button"></a>Как встраить кнопку "Поделиться" в Teams

Сначала необходимо добавить сценарий `launcher.js` на веб-страницу.

```html
<script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
```

Затем добавьте htmL-элемент на веб-страницу с атрибутом класса и ссылкой для совместной использования `teams-share-button` в `data-href` атрибуте.

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>">
</div>
```

Это добавит значок Microsoft Teams на ваш веб-сайт.

![Значок "Поделиться в Teams"](~/assets/icons/share-to-teams-icon.png)

При желании, если вы хотите использовать другой размер значка для кнопки "Поделиться в Teams", используйте `data-icon-px-size` атрибут.

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-icon-px-size="64">
</div>
```

Если вы знаете, что предварительный просмотр URL-адреса из ссылки для совместного просмотра не будет хорошо отрисовки в Teams (например, ссылка требует проверки подлинности пользователя), вы можете отключить предварительный просмотр URL-адресов, добавив атрибут, установленный в `data-preview` `false` .

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-preview="false">
</div>
```

Если страница динамически отрисовки содержимого, можно использовать метод для принудительного отображения кнопки "Поделиться" в соответствующем `shareToMicrosoftTeams.renderButtons()` месте конвейера. 

## <a name="crafting-your-website-preview"></a>Создайте предварительную версию веб-сайта

Когда ваш веб-сайт будет общим для Teams, карточка, вставленная в выбранный канал, будет содержать предварительный просмотр вашего веб-сайта. Вы можете управлять поведением этой предварительной версии, убедившись, что соответствующие метаданные добавлены на веб-сайт для общего просмотра `data-href` (URL-адрес). В таблице ниже описаны необходимые теги. Вы можете использовать либо версии html по умолчанию, либо версию Open Graph.

Чтобы предварительный просмотр отображался, необходимо:

* Включаем изображение эскиза или заголовок и описание (для наилучших результатов включаем все три).
* URL-адрес, к который требуется общий доступ, не может требовать проверки подлинности. Если вы по-прежнему можете поделиться им, но предварительный просмотр не будет создан.

|Значение|Метатег| Open Graph|
|----|----|----|
|Название|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|Описание|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|Эскиз| Нет |`<meta property="og:image" content="http://example.com/image.jpg">`|

## <a name="share-to-teams-for-education"></a>Совместное участие в Teams для образования

Преподавателям, использующим кнопку "Поделиться в Teams", будет предоставлен дополнительный параметр `Create an Assignment` . Это позволяет быстро создать назначение в выбранной команде на основе общей ссылки.

![Всплывающее всплывающее окна "Поделиться в Teams"](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a>Полное launcher.js определения

| Свойство | Атрибут HTML | Тип | По умолчанию | Описание |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| href | `data-href` | string | н/д | Href содержимого для совместной работы. |
| preview | `data-preview` | boolean (в качестве строки) | `true` | Следует ли показывать предварительный просмотр содержимого для демонстрации. |
| iconPxSize | `data-icon-px-size` | number (в строке) | `32` | Размер в пикселях кнопки share-to-Teams для отрисовки. |
| msgText | `data-msg-text` | string | н/д | Текст по умолчанию, вставляемый перед ссылкой в поле составить сообщение (ограничение в 200 символов) |
| assignInstr | `data-assign-instr` | string | н/д | Текст по умолчанию, вставляемый в поле "Инструкции" (ограничение в 200 символов) |
| assignTitle | `data-assign-title` | string | н/д | Текст по умолчанию, вставляемый в поле "Название" (ограничение в 50 символов) |

### <a name="methods"></a>Методы

**`shareToMicrosoftTeams.renderButtons(options)`**

`options` (необязательно): `{ elements?: HTMLElement[] }`

Отрисовка всех кнопок для совместной оказания услуг, которые в настоящее время находятся на странице. Если необязательный объект предоставляется со списком элементов, эти элементы будут отрисовыны в кнопки `options` для совместной работы.

### <a name="setting-default-form-values"></a>Установка значений формы по умолчанию

При желании вы можете установить значения по умолчанию для следующих полей в форме "Поделиться в Teams":

* Скажите что-нибудь об этом ( `msgText` )
* Инструкции по назначению ( `assignInstr` )
* Заголовок назначения ( `assignTitle` )

#### <a name="example-default-form-values"></a>Пример: значения форм по умолчанию

```html
<span
    class="teams-share-button"
    data-href="https://www.microsoft.com/education/products/teams"
    data-msg-text="Default Message"
    data-assign-title="Default Assignment Title"
    data-assign-instr="Default Assignment Instructions"
></span>
```
