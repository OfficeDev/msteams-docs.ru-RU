---
title: Предоставление общего доступа Teams из веб-приложений
description: Узнайте, как добавить общую папку Teams внедренную кнопку на веб-сайте с предварительным просмотром веб-сайта с помощью примеров кода
ms.topic: reference
ms.localizationpriority: medium
keywords: Предоставление общего Teams общий доступ Teams
ms.openlocfilehash: ac08d3c697bc5f02eb8527d2239afe022cb421af
ms.sourcegitcommit: f892125106adb6731a20127f15d6e92f279127c5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2022
ms.locfileid: "64685686"
---
# <a name="share-to-teams-from-web-apps"></a>Предоставление общего доступа Teams из веб-приложений

Сторонние веб-сайты могут использовать сценарий средства запуска для внедрения share в Teams кнопки на своих веб-страницах. При выборе этого параметра запускается общий доступ Teams во всплывающем окне. Это позволяет предоставлять общий доступ к ссылке непосредственно любому пользователю или Microsoft Teams каналу без переключения контекста. В этом документе описывается, как создать и внедрить общий ресурс в Teams веб-сайта, создать предварительный просмотр веб-сайта и расширить общий доступ Teams для образования.

> [!NOTE]
>
> * Поддерживаются только классические версии MicrosoftEdge&nbsp; и Google Chrome.
> * Использование учетных записей Freemium или гостевых учетных записей не поддерживается.  

На следующем рисунке показан общий доступ Teams интерфейса всплывающего окна:

:::image type="content" source="../../assets/images/share-to-teams-popup.png" alt-text="Всплывающее окно &quot;Поделиться Teams&quot;":::

## <a name="embed-a-share-to-teams-button"></a>Кнопка "Внедрить общую папку Teams"

1. Добавьте скрипт `launcher.js` на веб-страницу.

    ```html
    <script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
    ```

1. Добавьте элемент HTML на веб-страницу `teams-share-button` с атрибутом класса и ссылкой для совместного использования в атрибуте `data-href` .

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>">
    </div>
    ```

    После этого значок Microsoft Teams добавляется на ваш веб-сайт. На следующем рисунке показан значок "Поделиться Teams":

    ![Значок "Поделиться Teams"](~/assets/icons/share-to-teams-icon.png)

1. Кроме того, если требуется другой размер значка для кнопки "Общий доступ Teams", используйте атрибут`data-icon-px-size`.

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-icon-px-size="64">
    </div>
    ```

1. Если для общей ссылки требуется проверка подлинности пользователя, а предварительный просмотр URL-адреса из ссылки для общего доступа не будет хорошо отображаться в Teams, вы можете отключить предварительный просмотр URL-адресов `data-preview` `false`, добавив в него набор атрибутов.

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-preview="false">
    </div>
    ```

1. Если страница динамически отображает содержимое, можно использовать этот метод, `shareToMicrosoftTeams.renderButtons()` чтобы принудительно отобразить **общий** ресурс в нужном месте конвейера.

## <a name="craft-your-website-preview"></a>Создание предварительной версии веб-сайта

Когда ваш веб-сайт Teams, карточка, вставленная в выбранный канал, содержит предварительный просмотр веб-сайта. Вы можете управлять поведением этой предварительной версии, обеспечивая добавление соответствующих метаданных на общий веб-сайт, например URL-адрес `data-href` .  

Чтобы отобразить предварительный просмотр, скажите следующее:

* Необходимо включить **либо эскиз,** либо **заголовок и** **описание**. Для получения наилучших результатов включите все три.
* Общий URL-адрес не требует проверки подлинности. Если требуется проверка подлинности, вы можете поделиться с ней, но предварительная версия не будет создана.

В следующей таблице описаны необходимые теги:

|Значение|Метатег| Открыть Graph|
|----|----|----|
|Название|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|Описание|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|Миниатюру| Ни один. |`<meta property="og:image" content="http://example.com/image.jpg">`|

Можно использовать либо версии HTML по умолчанию, либо open Graph версии.

## <a name="share-to-teams-for-education"></a>Предоставление общего доступа Teams для образования

Для преподавателей, использующих кнопку "Общий доступ Teams", есть дополнительный параметр`Create an Assignment`. Это позволяет быстро создать назначение в выбранной команде на основе общей ссылки. На следующем рисунке показан общий доступ Teams для образовательных учреждений:

:::image type="content" source="../../assets/images/share-to-teams-popup-edu.png" alt-text="Предоставление общего доступа Teams образования":::

## <a name="full-launcherjs-definition"></a>Полное launcher.js определения

| Свойство | Атрибут HTML | Тип | По умолчанию | Описание |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| href | `data-href` | String | н/д | Href содержимого для совместного использования. |
| preview | `data-preview` | Логическое значение (в виде строки) | `true` | Указывает, следует ли отображать предварительный просмотр содержимого для совместного использования. |
| iconPxSize | `data-icon-px-size` | number (в виде строки) | `32` | Размер в пикселях общей папки, Teams для отрисовки. |
| msgText | `data-msg-text` | String | н/д | Текст по умолчанию, вставляемый перед ссылкой в поле создания сообщения. Максимальное число символов — 200. |
| assignInstr | `data-assign-instr` | String | н/д | Текст по умолчанию, вставляемый в поле "Инструкции" назначений. Максимальное число символов — 200. |
| assignTitle | `data-assign-title` | String | н/д | Текст по умолчанию, вставляемый в поле "Название". Максимальное число символов — 50. |

### <a name="methods"></a>Методы

**`shareToMicrosoftTeams.renderButtons(options)`**

`options` (необязательно): `{ elements?: HTMLElement[] }`

В настоящее время все кнопки общего доступа отображаются на странице. Если необязательный `options` объект предоставляется со списком элементов, эти элементы преобразуются в кнопки общего доступа.

### <a name="set-default-form-values"></a>Задание значений формы по умолчанию

Вы можете выбрать, чтобы задать значения по умолчанию для следующих полей в общей папке Teams форме:

* Скажите что-нибудь об этом: `msgText`
* Инструкции по назначению: `assignInstr`
* Заголовок назначения: `assignTitle`

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
* [Предоставление общего доступа Teams из личного приложения или вкладки](share-to-teams-from-personal-app-or-tab.md)
