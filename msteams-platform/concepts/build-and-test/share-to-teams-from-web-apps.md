---
title: Поделиться в Teams из веб-приложений
description: Узнайте, как добавить встроенную кнопку «Отправить в Teams» на веб-сайт с предварительным просмотром веб-сайта с помощью примеров кода
ms.topic: reference
ms.localizationpriority: medium
keywords: Отправить в Teams Отправка в Teams
ms.openlocfilehash: b3efd268e2bded3955c2d9ab76d6dea755d06b5a
ms.sourcegitcommit: a3567e3e1a52b8e3cb2072b037f0e75bd0f12e58
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/17/2022
ms.locfileid: "65439302"
---
# <a name="share-to-teams-from-web-apps"></a>Поделиться в Teams из веб-приложений

Сторонние веб-сайты могут использовать сценарий запуска для встраивания кнопок «Отправить в Teams» на свои веб-страницы. При выборе этого параметра запускается функция «Отправить в Teams» во всплывающем окне. Этот параметр позволяет поделиться ссылкой напрямую с любым человеком или каналом Microsoft Teams без переключения контекста. В этом документе описывается, как создать и внедрить кнопку «Отправить в Teams» на свой веб-сайт, создать предварительный просмотр веб-сайта и расширить возможности «Отправить в Teams для образования».

> [!NOTE]
>
> * Поддерживаются только настольные версии Microsoft&nbsp;Edge и Google Chrome.
> * Использование учетных записей Freemium или гостевых учетных записей не поддерживается.  

На следующем изображении отображается всплывающее окно "Отправить в Teams":

:::image type="content" source="../../assets/images/share-to-teams-popup.png" alt-text="Всплывающее окно «Отправить в Teams»":::

## <a name="embed-a-share-to-teams-button"></a>Внедрение кнопки «Отправить в Teams»

1. Добавьте сценарий `launcher.js` на веб-страницу.

    ```html
    <script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
    ```

1. Добавьте элемент HTML на свою веб-страницу с атрибутом класса `teams-share-button` и ссылкой для совместного использования в атрибуте `data-href`.

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>">
    </div>
    ```

    После этого на ваш веб-сайт будет добавлен значок Microsoft Teams. На следующем рисунке показан значок «Отправить в Teams»:

    ![Значок «Отправить в Teams»](~/assets/icons/share-to-teams-icon.png)

1. Кроме того, если требуется другой размер значка для кнопки "Отправить в Teams", используйте атрибут `data-icon-px-size`.

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-icon-px-size="64">
    </div>
    ```

1. Если для общей ссылки требуется проверка подлинности пользователя, а предварительный просмотр URL-адреса из ссылки для общего доступа не отображается в Teams, вы можете отключить предварительный просмотр URL-адреса, добавив атрибут `data-preview`, установленный в `false`.

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-preview="false">
    </div>
    ```

1. Чтобы отобразить выбранное сообщение в поле создания, можно определить текст в атрибуте `data-msg-text` .

     ```html
     <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-msg-text="<default-message-to-be-populated-in-compose-box>"
      data-preview="false">
      </div>
     ```

1. Если страница динамически отображает содержимое, можно использовать этот метод `shareToMicrosoftTeams.renderButtons()`, чтобы принудительно отображать **Отправить** в соответствующем месте конвейера.

## <a name="craft-your-website-preview"></a>Создание предварительной версии веб-сайта

При отправки веб-сайта в Teams, карточка, которая вставляется в выбранный канал, содержит предварительный просмотр вашего веб-сайта. Вы можете управлять поведением этого предварительного просмотра, обеспечив добавление соответствующих метаданных к совместно используемому веб-сайту, например URL-адрес `data-href`.  

Чтобы отобразить предварительную версию, выполните следующие действия:

* Необходимо включить либо **Эскиз**, либо **Заголовок** и **Описание**. Для достижения наилучших результатов включите все три параметра.
* Общий URL-адрес не требует проверки подлинности. Если для этого требуется аутентификация, вы можете поделиться им, но предварительная версия не создается.

В следующей таблице описаны необходимые теги:

|Значение|Метатег| Open Graph|
|----|----|----|
|Название|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|Описание|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|Эскиз| Нет. |`<meta property="og:image" content="http://example.com/image.jpg">`|

Можно использовать либо версии HTML по умолчанию, либо версию Open Graph.

## <a name="share-to-teams-for-education"></a>Предоставление общего доступа в Teams для образования

Для преподавателей, использующих кнопку "Отправить в Teams", есть дополнительный параметр `Create an Assignment`. Он позволяет быстро создать задание в выбранной команде на основе общей ссылки. На следующем изображении показан общий доступ к Teams для образования:

:::image type="content" source="../../assets/images/share-to-teams-popup-edu.png" alt-text="Всплывающее окно «Отправка в Teams для образования»":::

## <a name="full-launcherjs-definition"></a>Полное определение launcher.js

| Свойство | Атрибут HTML | Тип | По умолчанию | Описание |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| href | `data-href` | string | н/д | Href содержимого для совместного использования. |
| preview | `data-preview` | Логическое значение (в виде строки) | `true` | Указывает, следует ли отображать предварительный просмотр содержимого для совместного использования. |
| iconPxSize | `data-icon-px-size` | число (в виде строки) | `32` | Размер в пикселях кнопки «Отправить в Teams» для отображения. |
| msgText | `data-msg-text` | Строка | н/д | Текст по умолчанию, который будет вставлен перед ссылкой в поле создания сообщения. Максимальное количество символов — 200 |
| assignInstr | `data-assign-instr` | Строка | н/д | Текст по умолчанию для вставки в поле заданий «Инструкции». Максимальное количество символов — 200 |
| assignTitle | `data-assign-title` | Строка | н/д | Текст по умолчанию для вставки в поле заданий «Название». Максимальное количество символов — 50. |

### <a name="methods"></a>Методы

**`shareToMicrosoftTeams.renderButtons(options)`**

`options` (необязательно): `{ elements?: HTMLElement[] }`

В настоящее время все кнопки «Поделиться» отображаются на странице. Если необязательный объект `options` предоставляется со списком элементов, эти элементы отображаются в виде кнопок общего доступа.

### <a name="set-default-form-values"></a>Настройка значений формы по умолчанию

Вы можете настроить значения по умолчанию для следующих полей в форме «Отправить в Teams»:

* Прокомментируйте это: `msgText`
* Инструкции к заданию: `assignInstr`
* Название задания: `assignTitle`

#### <a name="example"></a>Пример

 Значения формы по умолчанию приведены в следующем примере:

```html
<span
    class="teams-share-button"
    data-href="https://www.microsoft.com/education/products/teams"
    data-msg-text="Default Message"
    data-assign-title="Default Assignment Title"
    data-assign-instr="Default Assignment Instructions"
></span>
```

## <a name="see-also"></a>Дополнительные ресурсы

* [Интеграция веб-приложений](~/samples/integrate-web-apps-overview.md)
* [Поделиться в Teams из личного приложения или вкладки](share-to-teams-from-personal-app-or-tab.md)
