---
title: Создание соединителей Office 365
author: laujan
description: Начало работы с Office 365 соединителями. Добавьте соединитель в приложение Teams в Microsoft Teams. Sample(.NET, Node.js) Office 365 connector, создающего уведомления в канал Teams.
ms.localizationpriority: medium
ms.topic: conceptual
ms.date: 06/16/2021
ms.openlocfilehash: 82fa425b3a2edb4db72c327655bdc8513d6b51f3
ms.sourcegitcommit: 176bbca74ba46b7ac298899d19a2d75087fb37c1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/04/2022
ms.locfileid: "68376580"
---
# <a name="create-office-365-connectors"></a>Создание соединителей Office 365

With Microsoft Teams apps, you can add your existing Office 365 Connector or build a new one within Teams. For more information, see [build your own connector](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector).

В следующем видео показано, как создать соединители Office 365.
<br>

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4OIzv]
<br>

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="add-a-connector-to-teams-app"></a>Добавление соединителя в приложение Teams

Вы можете создать [пакет](~/concepts/build-and-test/apps-package.md) и [опубликовать](~/concepts/deploy-and-publish/apps-publish.md) соединитель в рамках отправки в AppSource. Зарегистрированный соединитель можно распространять в составе пакета приложений Teams. Сведения о точках входа для приложения Teams см. в разделе [Возможности](~/concepts/extensibility-points.md). Вы также можете предоставить пакет пользователям напрямую для загрузки в Teams.

Чтобы распространить соединитель, зарегистрируйте его на [информационной панели разработчика соединителей](https://aka.ms/connectorsdashboard).

Чтобы соединитель можно было использовать только в Teams, следуйте инструкциям по отправке соединителя при публикации приложения в [microsoft Teams Store](~/concepts/deploy-and-publish/appsource/publish.md) . В противном случае зарегистрированный соединитель работает во всех продуктах Office 365, поддерживающих приложения, включая Outlook и Teams.

> [!IMPORTANT]
> Соединитель регистрируется после выбора **Сохранить** на информационной панели разработчика соединителей. Если вы хотите опубликовать свой соединитель в AppSource, следуйте инструкциям в статье [Публикация приложения Microsoft Teams в AppSource](~/concepts/deploy-and-publish/apps-publish.md). Если вы не хотите публиковать приложение в AppSource, распространяйте его непосредственно в организации. После публикации соединителей для организации никаких дополнительных действий на информационной панели соединителей не требуется.

### <a name="integrate-the-configuration-experience"></a>Интеграция возможностей настройки

Пользователи могут выполнять весь процесс настройки соединителя, не выходя из клиента Teams. Чтобы получить больше возможностей, Teams может внедрить вашу страницу конфигурации непосредственно в IFrame. Последовательность операций выглядит следующим образом:

1. Пользователь выбирает соединитель, чтобы начать процесс настройки.
1. Пользователь взаимодействует с веб-интерфейсом для завершения настройки.
1. Пользователь нажимает **Сохранить**, что вызывает обратный вызов в коде.

    > [!NOTE]
    >
    > * Код может обрабатывать событие сохранения, получая параметры веб-перехватчика. Код сохраняет веб-перехватчик для последующей публикации событий.
    > * Процесс настройки загружается в Teams.

Вы можете повторно использовать существующие возможности веб-настройки или создать отдельную версию для размещения специально в Teams. Код должен содержать пакет SDK JavaScript для Teams. Это предоставляет коду доступ к API для выполнения общих операций, таких как получение текущего пользователя, канала или контекста команды, а также запуск потоков проверки подлинности.

Чтобы интегрировать процесс конфигурации:

> [!NOTE]
> Начиная с версии 2.0.0.0 клиентского пакета SDK для JavaScript для Teams API в пространстве имен параметров устарели  в пользу эквивалентных API-интерфейсов в пространстве имен страниц,  `pages.getConfig()` включая и другие API-интерфейсы `pages.config` во вложенном пространстве имен. Дополнительные сведения см. в статье ["Новые возможности TeamsJS версии 2.0"](../../tabs/how-to/using-teams-client-sdk.md#whats-new-in-teamsjs-version-20).

1. Инициализация SDK происходит путем вызова `app.initialize()`.
1. Вызовите `pages.config.setValidityState(true)` для включения параметра **Сохранить**.

    > [!NOTE]
    > Необходимо вызвать `microsoftTeams.pages.config.setValidityState(true)` в ответ на выбор пользователя или обновление поля.

1. Зарегистрируйте обработчик событий `microsoftTeams.pages.config.registerOnSaveHandler()`, который будет вызван, когда пользователь выбирает **Сохранить**.
1. Call `microsoftTeams.pages.config.setConfig()` to save the connector settings. The saved settings are also shown in the configuration dialog if the user tries to update an existing configuration for your connector.
1. Вызовите `microsoftTeams.pages.getConfig()` для получения свойств веб-перехватчика, включая URL-адрес.

    > [!NOTE]
    > При первой загрузке страницы в случае перенастройки необходимо вызвать `microsoftTeams.pages.getConfig()`.

1. Зарегистрируйте обработчик событий `microsoftTeams.pages.config.registerOnRemoveHandler()`, который будет вызван, когда пользователь удаляет соединитель.

Это событие дает вашей службе возможность выполнять любые действия по очистке.

В следующем коде представлен пример HTML для создания страницы конфигурации соединителя без центра обслуживания клиентов и службы поддержки клиентов:

```html
<h2>Send notifications when tasks are:</h2>
<div class="col-md-8">
    <section id="configSection">
        <form id="configForm">
            <input type="radio" name="notificationType" value="Create" onclick="onClick()"> Created
            <br>
            <br>
            <input type="radio" name="notificationType" value="Update" onclick="onClick()"> Updated
        </form>
    </section>
</div>

<script src="https://res.cdn.office.net/teams-js/2.0.0/js/MicrosoftTeams.min.js" integrity="sha384-Q2Z9S56exI6Oz/ThvYaV0SUn8j4HwS8BveGPmuwLXe4CvCUEGlL80qSzHMnvGqee" crossorigin="anonymous"></script>
<script src="/Scripts/jquery-1.10.2.js"></script>

<script type="module">
        import {app, pages} from 'https://res.cdn.office.net/teams-js/2.0.0/js/MicrosoftTeams.min.js';
        
        function onClick() {
            pages.config.setValidityState(true);
        }

        await app.initialize();
        pages.config.registerOnSaveHandler(function (saveEvent) {
            var radios = document.getElementsByName('notificationType');

            var eventType = '';
            if (radios[0].checked) {
                eventType = radios[0].value;
            } else {
                eventType = radios[1].value;
            }

            await pages.config.setConfig({
                entityId: eventType,
                contentUrl: "https://YourSite/Connector/Setup",
                removeUrl:"https://YourSite/Connector/Setup",
                configName: eventType
                });

            pages.getConfig().then(async (config) {
                // We get the Webhook URL from config.webhookUrl which needs to be saved. 
                // This can be used later to send notification.
            });

            saveEvent.notifySuccess();
        });

        pages.config.registerOnRemoveHandler(function (removeEvent) {
            alert("Removed" + JSON.stringify(removeEvent));
        });

</script>
```

Чтобы проверить подлинность пользователя как часть загрузки вашей страницы, см. раздел [процесс проверки подлинности для вкладок](~/tabs/how-to/authentication/auth-flow-tab.md), чтобы интегрировать вход при настройке страницы.

> [!NOTE]
> До версии TeamsJS версии 2.0.0 код должен вызываться с использованием URL-адреса `authenticate()` и `microsoftTeams.authentication.registerAuthenticationHandlers()` методов обратного вызова успешного или неудачного вызова, прежде чем вызывать из-за совместимости между клиентами. Начиная с TeamsJS версии 2.0.0, *функция registerAuthenticationHandlers* не рекомендуется использовать для прямого вызова [authenticate()](/javascript/api/@microsoft/teams-js/authentication#@microsoft-teams-js-authentication-authenticate) с необходимыми параметрами проверки подлинности.

#### <a name="getconfig-response-properties"></a>Свойства ответа `getConfig`

>[!NOTE]
>Параметры, возвращаемые `getConfig` вызовом, отличаются при вызове этого метода из вкладки и отличаются от параметров, задокументированных в [ссылке](/javascript/api/@microsoft/teams-js/pages#@microsoft-teams-js-pages-getconfig).

В следующей таблице представлены параметры и сведения о свойствах ответа `getConfig`:

| Параметры   | Details |
|-------------|---------|
| `entityId`       | Идентификатор сущности, который задается кодом при вызове `setConfig()`. |
| `configName`  | Имя конфигурации, заданное кодом при вызове `setConfig()`. |
| `contentUrl` | URL-адрес страницы конфигурации, заданный кодом при вызове `setConfig()`. |
| `webhookUrl` | The webhook URL created for the connector. Use the webhook URL to POST structured JSON to send cards to the channel. The `webhookUrl` is returned only when the application returns data successfully. |
| `appType` | Возвращаемые значения могут быть `mail`или `groups``teams` соответствующими Office 365 почты, Office 365 групп или Teams соответственно. |
| `userObjectId` | The unique ID corresponding to the Office 365 user who initiated the set up of the connector. It must be secured. This value can be used to associate the user in Office 365, who has set up the configuration in your service. |

#### <a name="handle-edits"></a>Обработка изменений

Код должен обрабатывать пользователей, которые возвращаются для изменения существующей конфигурации соединителя. Для этого вызовите `microsoftTeams.pages.config.setConfig()` во время начальной настройки со следующими параметрами:

* `entityId` — это настраиваемый идентификатор, который представляет то, что пользователь настроил и понял с помощью службы.
* `configName` — это имя, которое может получить код конфигурации.
* `contentUrl` — это настраиваемый URL-адрес, который загружается, когда пользователь изменяет существующую конфигурацию соединителя.

Этот вызов выполняется как часть обработчика событий сохранения. Затем при загрузке `contentUrl` код должен вызвать `getConfig()` для предварительного заполнения любых параметров или форм в пользовательском интерфейсе конфигурации.

#### <a name="handle-removals"></a>Обработка удалений

Обработчик событий можно выполнить, когда пользователь удаляет существующую конфигурацию соединителя. Этот обработчик регистрируется путем вызова `microsoftTeams.pages.config.registerOnRemoveHandler()`. Этот обработчик используется для выполнения операций очистки, таких как удаление записей из базы данных.

### <a name="include-the-connector-in-your-manifest"></a>Включение соединителя в манифест

Скачайте автоматически созданный *манифест приложения Teams* с портала разработчика (<https://dev.teams.microsoft.com>). Выполните следующие шаги перед проверкоц или публикацией приложения:

1. [Включение двух значков](../../concepts/build-and-test/apps-package.md#app-icons).
1. Измените раздел `icons` манифеста, чтобы включить имена файлов значков вместо URL-адресов.

Следующий файл *manifest.json* содержит элементы, необходимые для тестирования и отправки приложения:

> [!NOTE]
> Замените `id` и `connectorId` в приведенном ниже примере на глобальный уникальный ИД соединителя.

#### <a name="example-of-manifestjson-with-connector"></a>Пример manifest.json с соединителем

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "id": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
  "version": "1.0",
  "developer": {
    "name": "Publisher",
    "websiteUrl": "https://www.microsoft.com",
    "privacyUrl": "https://www.microsoft.com",
    "termsOfUseUrl": "https://www.microsoft.com"
  },
  "description": {
    "full": "This is a small sample app we made for you! This app has samples of all capabilities Microsoft Teams supports.",
    "short": "This is a small sample app we made for you!"
  },
  "icons": {
    "outline": "sampleapp-outline.png",
    "color": "sampleapp-color.png"
  },
  "connectors": [
    {
      "connectorId": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
      "scopes": [
        "team"
      ]
    }
  ],
  "name": {
    "short": "Sample App",
    "full": "Sample App"
  },
  "accentColor": "#FFFFFF",
  "needsIdentity": "true"
}
```

## <a name="test-your-connector"></a>Проверка соединители

To test your connector, upload it to a team with any other app. You can create a .zip package using the manifest file from the two icon files and connectors Developer Dashboard, modified as directed in [Include the connector in your Manifest](#include-the-connector-in-your-manifest).

После отправки приложения откройте список соединителей с любого канала. Прокрутите вниз, чтобы найти свое приложение в разделе **Отправленные**.

![Снимок экрана раздела отправленных приложений в диалоговом окне соединителя](~/assets/images/connectors/connector_dialog_uploaded.png)

> [!NOTE]
> Поток полностью выполняется в Teams в качестве размещенного интерфейса.

Чтобы убедиться, что действие `HttpPOST` работает правильно, [отправьте сообщения в свой соединитель](~/webhooks-and-connectors/how-to/connectors-using.md).

Выполните [пошаговое руководство по](../../sbs-teams-connectors.yml) созданию и проверке соединителей в Teams.

## <a name="distribute-webhook-and-connector"></a>Распространение веб-перехватчика и соединителя

1. [Настройте входящий веб-перехватчик](~/webhooks-and-connectors/how-to/add-incoming-webhook.md#create-an-incoming-webhook) непосредственно для своей команды.

1. Добавьте [страницу конфигурации](~/webhooks-and-connectors/how-to/connectors-creating.md?#integrate-the-configuration-experience) и опубликуйте входящий веб-перехватчик в Office 365 connector.

1. Упакуйте и опубликуйте свой соединитель как часть отправки в [AppSource](~/concepts/deploy-and-publish/office-store-guidance.md).

## <a name="code-sample"></a>Пример кода

В следующей таблице приведены имя примера и его описание:

|**Название примера** | **Описание** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| Connectors | Пример соединителя Office 365, создающий уведомления для канала Teams.| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-todo-notification/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-github-notification/nodejs)|
| Пример универсальных соединителей |Пример кода универсального соединителя, который легко настроить для любой системы, поддерживающей веб-перехватчики.| | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-generic/nodejs)|

## <a name="step-by-step-guide"></a>Пошаговые инструкции

Следуйте [пошаговым инструкциям](../../sbs-teams-connectors.yml) для создания и тестирования соединителя в Teams.

## <a name="see-also"></a>Дополнительные ресурсы

* [Создание и отправка сообщений](~/webhooks-and-connectors/how-to/connectors-using.md)
* [Создание входящего веб-перехватчика](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [Создание соединителя Office 365](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [Включение и отключение соединителей администраторами](/MicrosoftTeams/office-365-custom-connectors#enable-or-disable-connectors-in-teams)
* [Публикация настраиваемых соединителей администраторами в своей организации](/MicrosoftTeams/office-365-custom-connectors)
* [Создание бота уведомлений с помощью JavaScript](../../sbs-gs-notificationbot.yml)
* [Создание первого приложения бота с помощью JavaScript](../../sbs-gs-bot.yml)
