---
title: Создать страницу конфигурации
author: laujan
description: создание страницы конфигурации.
keywords: Настраиваемый канал группы вкладок teams
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 2544454fd06348fa41269f3a8fd57cc71a07d140
ms.sourcegitcommit: 84f408aa2854aa7a5cefaa66ce9a373b19e0864a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/18/2021
ms.locfileid: "49886739"
---
# <a name="create-a-configuration-page"></a>Создать страницу конфигурации

Страница конфигурации — это специальный тип страницы [контента.](content-page.md) Пользователи настраивают некоторые аспекты приложения Microsoft Teams на странице конфигурации и используют эту конфигурацию в составе следующих ключевых моментов:

* Вкладка канала или группового чата — сбор сведений от пользователей и настройка `contentUrl` отображаемой страницы содержимого.
* Расширение [для обмена сообщениями](~/messaging-extensions/what-are-messaging-extensions.md)
* [Соединители Office 365](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)

## <a name="configuring-a-channel-or-group-chat-tab"></a>Настройка вкладки чата канала или группы

Приложение должно ссылаться на [клиентский SDK JavaScript для Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) и вызывать `microsoft.initialize()` его. Кроме того, используемые URL-адреса должны быть защищены конечными точками HTTPS и доступны из облака. Ниже приводится пример страницы конфигурации.

```html
<head>
<script src='https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js'></script>
</head>
    <body>
        <button onclick="(document.getElementById('icon').src = '/images/iconGray.png'); colorClickGray()">Select Gray</button>
        <img id="icon" src="/images/teamsIcon.png" alt="icon" style="width:100px" />
        <button onclick="(document.getElementById('icon').src = '/images/iconRed.png'); colorClickRed()">Select Red</button>

        <script>
            microsoftTeams.initialize();
            let saveGray = () => {
                microsoftTeams.settings.registerOnSaveHandler((saveEvent) => {
                    microsoftTeams.settings.setSettings({
                        websiteUrl: "https://yourWebsite.com",
                        contentUrl: "https://yourWebsite.com/gray",
                        entityId: "grayIconTab",
                        suggestedDisplayName: "MyNewTab"
                    });
                    saveEvent.notifySuccess();
                });
            }
            let saveRed = () => {
                microsoftTeams.settings.registerOnSaveHandler((saveEvent) => {
                    microsoftTeams.settings.setSettings({
                        websiteUrl: "https://yourWebsite.com",
                        contentUrl: "https://yourWebsite.com/red",
                        entityId: "redIconTab",
                        suggestedDisplayName: "MyNewTab"
                    });
                    saveEvent.notifySuccess();
                });
            }

            let gr = document.getElementById("gray").style;
            let rd = document.getElementById("red").style;

            const colorClickGray = () => {
                gr.display = "block";
                rd.display = "none";
                microsoftTeams.settings.setValidityState(true);
                saveGray()
            }

            const colorClickRed = () => {
                rd.display = "block";
                gr.display = "none";
                microsoftTeams.settings.setValidityState(true);
                saveRed();
            }
        </script>
    </body>
...
```

На странице конфигурации выберите "Выбрать **серый"** или "Красный", чтобы отобразить содержимое вкладки с серым или красным значком.  Если нажать относительную кнопку, будет либо активна, либо будет `saveGray()` `saveRed()` вызвано следующее:

1. За `settings.setValidityState(true)` установлено true.
1. `microsoftTeams.settings.registerOnSaveHandler()`Инициирует обработник событий.
1. **Кнопка** "Сохранить" на странице конфигурации приложения, загруженная в Teams, включена.

Код страницы конфигурации информирует Teams о том, что требования к конфигурации выполнены и установка может продолжиться. Когда пользователь выбирает параметр **"Сохранить",** устанавливаются `settings.setSettings()` параметры, определенные `Settings` интерфейсом. Дополнительные сведения см. в [интерфейсе "Параметры".](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true) На последнем этапе будет вызвано, чтобы указать, что `saveEvent.notifySuccess()` URL-адрес контента успешно разрешен.

>[!NOTE]
>
>* Если вы регистрируете обработчивель сохранения с помощью, то метод callback должен вызвать или указать `microsoftTeams.settings.registerOnSaveHandler()` `saveEvent.notifySuccess()` результат `saveEvent.notifyFailure()` настройки.
>* Если вы не зарегистрируете обработок сохранения, вызов будет выполнен автоматически, когда пользователь `saveEvent.notifySuccess()` наберет **"Сохранить".**

### <a name="get-context-data-for-your-tab-settings"></a>Получить контекстные данные для параметров вкладок

Для отображения релевантной информации на вкладке может потребоваться контекстная информация. Контекстная информация еще больше повышает привлекательность вкладки, обеспечивая более настраиваемый пользовательский интерфейс.

Дополнительные сведения о свойствах, используемых для настройки вкладок, см. в [контекстных интерфейсах.](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) Соберйте значения переменных данных контекста двумя способами:

1. Вставьте в манифесте строки запроса `configurationURL` URL-адреса.

1. Используйте метод [Teams SDK.](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})`

#### <a name="insert-placeholders-in-the-configurationurl"></a>Вставка в них заме- `configurationUrl`

Добавьте в базу подстроки контекстного `configurationUrl` интерфейса. Например:

##### <a name="base-url"></a>Базовый URL-адрес

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a>Базовый URL-адрес со строками запроса

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

После отправки страницы Teams обновляет заметивые строки запроса соответствующими значениями. Включить логику на странице конфигурации для получения и использования этих значений. Дополнительные сведения о работе со строками запросов URL-адресов см. в [urlSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) в веб-документы MDN. В следующем примере описывается способ извлечения значения из `configurationUrl` свойства:

```html
<script>
   microsoftTeams.initialize();
   const getId = () => {
        let urlParams = new URLSearchParams(document.location.search.substring(1));
        let blueTeamId = urlParams.get('team');
        return blueTeamId
    }
//For testing, you can invoke the following to view the pertinent value:
document.write(getId());
</script>
```

### <a name="use-the-getcontext-function-to-retrieve-context"></a>Использование `getContext()` функции для извлечения контекста

Функция `microsoftTeams.getContext((context) => {})` извлекает интерфейс [контекста](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) при вызове. Добавьте эту функцию на страницу конфигурации для получения значений контекста:

```html
<!-- `userPrincipalName` will render in the span with the id "user". -->

<span id="user"></span>
...
<script>
    microsoftTeams.getContext((context) =>{
        let userId = document.getElementById('user');
        userId.innerHTML = context.userPrincipalName;
    });
</script>
...
```

## <a name="context-and-authentication"></a>Контекст и проверка подлинности

 Проверка подлинности перед разрешением пользователю настроить приложение. В противном случае контент может включать источники с протоколами проверки подлинности. Дополнительные сведения см. в [записи "Проверка подлинности пользователя на вкладке Microsoft Teams".](~/tabs/how-to/authentication/auth-flow-tab.md) Используйте контекстные сведения для создания запросов проверки подлинности и URL-адресов страниц авторизации.
Убедитесь, что в массиве указаны все домены, используемые на страницах `manifest.json` `validDomains` вкладок.

## <a name="modify-or-remove-a-tab"></a>Изменение или удаление вкладки

Поддерживаемые варианты удаления дополнительно уточняют пользовательский интерфейс. Задайте свойству манифеста свойство , которое позволяет пользователям изменять, перенастройку или переименовывать группу или `canUpdateConfiguration` `true` вкладку канала. Кроме того, указать, что происходит с содержимым при удалении вкладки, включив страницу параметров удаления в приложение и задав значение свойства `removeUrl` в  `setSettings()` конфигурации. Дополнительные сведения см. в [мобильных клиентах.](#mobile-clients) Пользователь может удалить личные вкладки, но не может изменять их. Дополнительные сведения см. в [подсети "Создание страницы удаления".](~/tabs/how-to/create-tab-pages/removal-page.md)

## <a name="mobile-clients"></a>Мобильные приложения

Если вы хотите, чтобы вкладка канала или группы появлялась на мобильных клиентах Teams, конфигурация должна иметь значение `setSettings()` `websiteUrl` свойства. Дополнительные сведения см. [в инструкциях для вкладок на мобильных устройствах.](~/tabs/design/tabs-mobile.md)

Конфигурация Microsoft Teams setSettings() для страницы удаления или мобильных клиентов:

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "URL REQUIRED FOR MOBILE CLIENTS",
    removeUrl: "ADD REMOVAL PAGE URL HERE"
});
```
