---
title: Создание кнопки «Поделиться в Teams»
description: Добавление встраиваемой кнопки Share Teams на веб-сайте
ms.topic: reference
ms.localizationpriority: medium
keywords: Совместное Teams share-to-Teams
ms.openlocfilehash: 0d0fb0d7baf18038cfe87b648d2550bbd20b593a
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/12/2021
ms.locfileid: "59156150"
---
# <a name="create-share-to-teams-button"></a>Создание кнопки «Поделиться в Teams»

Сторонние веб-сайты могут использовать сценарий запуска для встраив кнопки Share-to-Teams на своих веб-сайтах. При выборе в всплывающее окно запускается Teams share-to-Teams. Это позволяет обмениваться ссылками напрямую с любым Microsoft Teams каналом без переключения контекста. В этом документе вы можете узнать, как создать и встраить кнопку Share-to-Teams для веб-сайта, создать предварительный просмотр веб-сайта и расширить возможности share-to-Teams для образования.

> [!NOTE]
> * Поддерживаются только настольные версии Edge и Chrome.
> * Использование учетных записей Freemium или гостевой не поддерживается.  

На следующем изображении отображается всплывающее Teams share-to-Teams:

![Всплывающее Teams](~/assets/images/share-to-teams-popup.png)

## <a name="embed-a-share-to-teams-button"></a>Встраить кнопку Share в Teams

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

    После этого значок Microsoft Teams на ваш веб-сайт. На следующем изображении показан значок Share-to-Teams:

    ![Share to Teams icon](~/assets/icons/share-to-teams-icon.png)

1. Кроме того, если для кнопки Share-to-Teams нужен другой размер значка, используйте `data-icon-px-size` атрибут.

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-icon-px-size="64">
    </div>
    ```
1. Если общая ссылка требует проверки подлинности пользователей, а предварительный просмотр URL-адреса из общего доступного url-адреса не будет хорошо отрисовки Teams, то можно отключить предварительный просмотр URL-адреса, добавив набор атрибутов. `data-preview` `false`

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-preview="false">
    </div>
    ```

1. Если страница динамически отрисовки контента, вы можете использовать метод, чтобы заставить Share отрисовки `shareToMicrosoftTeams.renderButtons()` в соответствующем месте в конвейере. 

## <a name="craft-your-website-preview"></a>Создайте предварительный просмотр веб-сайта

Когда веб-сайт Teams, карта, вставленная в выбранный канал, содержит предварительный просмотр веб-сайта. Вы можете управлять поведением этого предварительного просмотра, обеспечивая добавление соответствующих метаданных на общий веб-сайт, например `data-href` URL-адрес.  

**Отображение предварительного просмотра**

* Вы должны включить либо **изображение эскиза**, или как **название и** **описание**. Для наилучших результатов включаем все три.
* Общий URL-адрес не требует проверки подлинности. Если для этого требуется проверка подлинности, вы можете поделиться им, но предварительный просмотр не создан.

В следующей таблице описаны необходимые теги:

|Значение|Метатег| Откройте Graph|
|----|----|----|
|Название|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|Описание|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|Эскиз изображения| нет. |`<meta property="og:image" content="http://example.com/image.jpg">`|

Вы можете использовать версии по умолчанию HTML или open Graph версии.

## <a name="share-to-teams-for-education"></a>Share to Teams для образования

Для учителей, использующих кнопку Share Teams, существует дополнительный параметр `Create an Assignment` . Это позволяет быстро создавать назначение в выбранной команде на основе общей ссылки. На следующем изображении отображается раздел share-to-Teams для образования: 

![Совместное Teams всплывающее образование](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a>Полное launcher.js определение

| Свойство | Атрибут HTML | Тип | По умолчанию | Описание |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| href | `data-href` | string | н/д | Href контента для обмена. |
| preview | `data-preview` | boolean (как строка) | `true` | Следует ли показывать предварительный просмотр контента для обмена. |
| iconPxSize | `data-icon-px-size` | номер (в качестве строки) | `32` | Размер пикселей кнопки share-to-Teams для отрисовки. |
| msgText | `data-msg-text` | string | н/д | Текст по умолчанию должен быть вставлен перед ссылкой в поле составить сообщение. Максимальное число символов — 200. |
| assignInstr | `data-assign-instr` | string | н/д | Текст по умолчанию, который будет вставлен в поле "Инструкции". Максимальное число символов — 200. |
| assignTitle | `data-assign-title` | string | н/д | Текст по умолчанию, который будет вставлен в поле "Title". Максимальное число символов — 50. |

### <a name="methods"></a>Методы

**`shareToMicrosoftTeams.renderButtons(options)`**

`options` (необязательный): `{ elements?: HTMLElement[] }`

В настоящее время все кнопки обмена отрисовка на странице. Если необязательный объект снабжен списком элементов, эти элементы `options` отрисовыются в кнопки share.

### <a name="set-default-form-values"></a>Настройка значений форм по умолчанию

Вы можете выбрать для набора значений по умолчанию для следующих полей в share Teams форме:

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
