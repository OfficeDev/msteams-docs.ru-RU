---
title: Создание кнопки «Поделиться в Teams»
description: Добавление встроенной кнопки Share to Teams на веб-сайте
ms.topic: reference
localization_priority: Normal
keywords: Share Teams Share-to-Teams
ms.openlocfilehash: d3e23c50cbaa38a53fa02c19cec69061478d9a57
ms.sourcegitcommit: d90c5dafea09e2893dea8da46ee49516bbaa04b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2021
ms.locfileid: "52075649"
---
# <a name="create-share-to-teams-button"></a>Создание кнопки «Поделиться в Teams»

Сторонние веб-сайты могут использовать сценарий запуска для встраив кнопки Share-to-Teams на своих веб-сайтах. При выборе запускается опыт share-to-Teams в всплывающее окно. Это позволяет обмениваться ссылками напрямую с любым человеком или каналом Microsoft Teams без переключения контекста. В этом документе вы можете узнать, как создать и встраить кнопку Share-to-Teams для веб-сайта, создать предварительный просмотр веб-сайта и расширить возможности share-to-Teams для образования.

> [!NOTE]
> * Поддерживаются только настольные версии Edge и Chrome.
> * Использование учетных записей Freemium или гостевой не поддерживается.  

На следующем изображении отображается всплывающее представление share-to-Teams:

![Всплывающее всплыв](~/assets/images/share-to-teams-popup.png)

## <a name="embed-a-share-to-teams-button"></a>Встраить кнопку Share to Teams

1. Добавьте `launcher.js` скрипт на веб-страницу.

    ```html
    <script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
    ```

1. Добавьте элемент HTML на веб-страницу с атрибутом класса и ссылкой, `teams-share-button` которая будет делиться в `data-href` атрибуте.

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>">
    </div>
    ```

    После завершения этого значка Microsoft Teams добавляется на ваш веб-сайт. На следующем изображении показан значок Share-to-Teams:

    ![Share to Teams icon](~/assets/icons/share-to-teams-icon.png)

1. Кроме того, если для кнопки Share-to Teams нужен другой размер значка, используйте `data-icon-px-size` атрибут.

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-icon-px-size="64">
    </div>
    ```
1. Если общая ссылка требует проверки подлинности пользователя, а предварительный просмотр URL-адреса из общей ссылки не будет хорошо отрисовки в Teams, можно отключить предварительный просмотр URL-адреса, добавив набор `data-preview` `false` атрибутов.

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-preview="false">
    </div>
    ```

1. Если на странице динамически отрисовка контента, можно использовать метод, чтобы заставить кнопку Share отрисовки в нужном месте `shareToMicrosoftTeams.renderButtons()` в конвейере. 

## <a name="craft-your-website-preview"></a>Создайте предварительный просмотр веб-сайта

Когда веб-сайт является общим для Teams, карта, вставленная в выбранный канал, содержит предварительный просмотр веб-сайта. Вы можете управлять поведением этого предварительного просмотра, обеспечивая добавление соответствующих метаданных на общий веб-сайт, например `data-href` URL-адрес.  

**Отображение предварительного просмотра**

* Вы должны включить либо **изображение эскиза**, или как **название и** **описание**. Для наилучших результатов включаем все три.
* Общий URL-адрес не требует проверки подлинности. Если для этого требуется проверка подлинности, вы можете поделиться им, но предварительный просмотр не создан.

В следующей таблице описаны необходимые теги:

|Значение|Метатег| Open Graph|
|----|----|----|
|Название|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|Описание|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|Эскиз изображения| нет. |`<meta property="og:image" content="http://example.com/image.jpg">`|

Можно использовать либо html-версии по умолчанию, либо версию Open Graph.

## <a name="share-to-teams-for-education"></a>Share to Teams for Education

Для преподавателей, использующих кнопку Share to Teams, существует дополнительный параметр `Create an Assignment` . Это позволяет быстро создавать назначение в выбранной команде на основе общей ссылки. На следующем изображении отображается share-to-Teams для образования: 

![Share to Teams popup education](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a>Полное launcher.js определение

| Свойство | Атрибут HTML | Тип | По умолчанию | Описание |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| href | `data-href` | Строка | н/д | Href контента для обмена. |
| preview | `data-preview` | boolean (как строка) | `true` | Следует ли показывать предварительный просмотр контента для обмена. |
| iconPxSize | `data-icon-px-size` | номер (в качестве строки) | `32` | Размер пикселей кнопки Share-to-Teams для отрисовки. |
| msgText | `data-msg-text` | Строка | н/д | Текст по умолчанию должен быть вставлен перед ссылкой в поле для составить сообщение. Максимальное число символов — 200. |
| assignInstr | `data-assign-instr` | Строка | н/д | Текст по умолчанию, который будет вставлен в поле "Инструкции". Максимальное число символов — 200. |
| assignTitle | `data-assign-title` | Строка | н/д | Текст по умолчанию, который будет вставлен в поле "Title". Максимальное число символов — 50. |

### <a name="methods"></a>Методы

**`shareToMicrosoftTeams.renderButtons(options)`**

`options` (необязательный): `{ elements?: HTMLElement[] }`

В настоящее время все кнопки обмена отрисовка на странице. Если необязательный объект снабжен списком элементов, эти элементы `options` отрисовыются в кнопки share.

### <a name="set-default-form-values"></a>Настройка значений форм по умолчанию

Можно выбрать для набора значений по умолчанию для следующих полей в форме Share to Teams:

* Скажите что-нибудь об этом: `msgText`
* Инструкции по назначению: `assignInstr`
* Название назначения: `assignTitle`

#### <a name="example"></a>Пример

 Значения форм по умолчанию даются в следующем примере:

```html
<span
    class="teams-share-button"
    data-href="https://www.microsoft.com/education/products/teams"
    data-msg-text="Default Message"
    data-assign-title="Default Assignment Title"
    data-assign-instr="Default Assignment Instructions"
></span>
```

## <a name="see-also"></a>См. также

[Интеграция веб-приложений](~/samples/integrate-web-apps-overview.md)
