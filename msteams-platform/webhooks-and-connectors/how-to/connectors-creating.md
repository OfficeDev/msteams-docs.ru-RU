---
title: Создание соединителей Office 365
author: laujan
description: Сведения о том, как начать работу с соединителями Office 365 в Microsoft Teams
keywords: Соединитель Office 365 в Teams
ms.localizationpriority: medium
ms.topic: conceptual
ms.date: 06/16/2021
ms.openlocfilehash: 2d711821d2b76b4cc2fd93a6d28cd5061129222e
ms.sourcegitcommit: 12510f34b00bfdd0b0e92d35c8dbe6ea1f6f0be2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/11/2022
ms.locfileid: "66032954"
---
# <a name="create-office-365-connectors"></a>Создание соединителей Office 365

С помощью приложений Microsoft Teams вы можете добавить существующий соединитель Office 365 или создать новый в Teams. Дополнительные сведения см. в разделе [Создание собственного соединителя](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector).

## <a name="add-a-connector-to-teams-app"></a>Добавление соединителя в приложение Teams

Вы можете создать [пакет](~/concepts/build-and-test/apps-package.md) и [опубликовать](~/concepts/deploy-and-publish/apps-publish.md) соединитель в рамках отправки в AppSource. Зарегистрированный соединитель можно распространять в составе пакета приложений Teams. Сведения о точках входа для приложения Teams см. в разделе [Возможности](~/concepts/extensibility-points.md). Вы также можете предоставить пакет пользователям напрямую для загрузки в Teams.

Чтобы распространить соединитель, зарегистрируйте его на [информационной панели разработчика соединителей](https://aka.ms/connectorsdashboard).

Чтобы соединитель можно было использовать только в Microsoft Teams, следуйте инструкциям по отправке соединителя в статье [Публикация приложения в магазине Microsoft Teams.](~/concepts/deploy-and-publish/appsource/publish.md). В противном случае зарегистрированный соединитель работает во всех продуктах Office 365, поддерживающих приложения, включая Outlook и Teams.

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

Вы можете повторно использовать существующие возможности веб-настройки или создать отдельную версию для размещения специально в Teams. Код должен содержать пакет SDK для JavaScript для Microsoft Teams. Это предоставляет коду доступ к API для выполнения общих операций, таких как получение текущего пользователя, канала или контекста группы и запуск потоков проверки подлинности.

Чтобы интегрировать процесс конфигурации:

1. Инициализация SDK происходит путем вызова `microsoftTeams.initialize()`.
1. Вызовите `microsoftTeams.settings.setValidityState(true)` для включения параметра **Сохранить**.

    > [!NOTE]
    > Необходимо вызвать `microsoftTeams.settings.setValidityState(true)` в ответ на выбор пользователя или обновление поля.

1. Зарегистрируйте обработчик событий `microsoftTeams.settings.registerOnSaveHandler()`, который будет вызван, когда пользователь выбирает **Сохранить**.
1. Вызовите `microsoftTeams.settings.setSettings()`, чтобы сохранить настройки коннектора. Сохраненные настройки также отображаются в диалоговом окне конфигурации, если пользователь пытается обновить существующую конфигурацию вашего соединителя.
1. Вызовите `microsoftTeams.settings.getSettings()` для получения свойств веб-перехватчика, включая URL-адрес.

    > [!NOTE]
    > При первой загрузке страницы в случае перенастройки необходимо вызвать `microsoftTeams.settings.getSettings()`.

1. Зарегистрируйте обработчик событий `microsoftTeams.settings.registerOnRemoveHandler()`, который будет вызван, когда пользователь удаляет соединитель.

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

<script src="https://statics.teams.microsoft.com/sdk/v1.5.2/js/MicrosoftTeams.min.js" crossorigin="anonymous"></script>
<script src="/Scripts/jquery-1.10.2.js"></script>

<script type="text/javascript">

        function onClick() {
            microsoftTeams.settings.setValidityState(true);
        }

        microsoftTeams.initialize();
        microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
            var radios = document.getElementsByName('notificationType');

            var eventType = '';
            if (radios[0].checked) {
                eventType = radios[0].value;
            } else {
                eventType = radios[1].value;
            }

            microsoftTeams.settings.setSettings({
                 entityId: eventType,
                contentUrl: "https://YourSite/Connector/Setup",
                removeUrl:"https://YourSite/Connector/Setup",
                 configName: eventType
                });

            microsoftTeams.settings.getSettings(function (settings) {
                // We get the Webhook URL in settings.webhookUrl which needs to be saved. 
                // This can be used later to send notification.
            });

            saveEvent.notifySuccess();
        });

        microsoftTeams.settings.registerOnRemoveHandler(function (removeEvent) {
            alert("Removed" + JSON.stringify(removeEvent));
        });

</script>
```

Чтобы проверить подлинность пользователя как часть загрузки вашей страницы, см. раздел [процесс проверки подлинности для вкладок](~/tabs/how-to/authentication/auth-flow-tab.md), чтобы интегрировать вход при настройке страницы.

> [!NOTE]
> Из соображений совместимости между клиентами ваш код должен вызывать `microsoftTeams.authentication.registerAuthenticationHandlers()` с помощью URL-адреса и методов успешного или неудачного обратного вызова перед вызовом `authenticate()`.

#### <a name="getsettings-response-properties"></a>Свойства ответа `GetSettings`

>[!NOTE]
>Параметры, возвращаемые вызовом `getSettings`, отличаются при вызове этого метода из вкладки и отличаются от задокументированных в [параметрах js](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings).

В следующей таблице представлены параметры и сведения о свойствах ответа `GetSetting`:

| Параметры   | Details |
|-------------|---------|
| `entityId`       | Идентификатор сущности, который задается кодом при вызове `setSettings()`. |
| `configName`  | Имя конфигурации, заданное кодом при вызове `setSettings()`. |
| `contentUrl` | URL-адрес страницы конфигурации, заданный кодом при вызове `setSettings()`. |
| `webhookUrl` | URL-адрес веб-перехватчика, созданный для соединителя. Используйте URL-адрес веб-перехватчика для POST структурированного JSON для отправки карточек на канал. `webhookUrl` возвращается только тогда, когда приложение успешно возвращает данные. |
| `appType` | Возвращаемыми значениями могут быть `mail`, `groups` или `teams` (для почты Office 365, групп Office 365 и Microsoft Teams соответственно). |
| `userObjectId` | Уникальный идентификатор, соответствующий пользователю Office 365, который инициировал настройку соединителя. Он должен быть безопасен. Это значение можно использовать для связывания пользователя в Office 365, который настроил конфигурацию в вашей службе. |

#### <a name="handle-edits"></a>Обработка изменений

Код должен обрабатывать пользователей, которые возвращаются для изменения существующей конфигурации соединителя. Для этого вызовите `microsoftTeams.settings.setSettings()` во время начальной настройки со следующими параметрами:

* `entityId` — это настраиваемый идентификатор, который представляет то, что пользователь настроил и понял с помощью службы.
* `configName` — это имя, которое может получить код конфигурации.
* `contentUrl` — это настраиваемый URL-адрес, который загружается, когда пользователь изменяет существующую конфигурацию соединителя.

Этот вызов выполняется как часть обработчика событий сохранения. Затем при загрузке `contentUrl` код должен вызвать `getSettings()` для предварительного заполнения любых параметров или форм в пользовательском интерфейсе конфигурации.

#### <a name="handle-removals"></a>Обработка удалений

Обработчик событий можно выполнить, когда пользователь удаляет существующую конфигурацию соединителя. Этот обработчик регистрируется путем вызова `microsoftTeams.settings.registerOnRemoveHandler()`. Этот обработчик используется для выполнения операций очистки, таких как удаление записей из базы данных.

### <a name="include-the-connector-in-your-manifest"></a>Включение соединителя в манифест

Скачайте автоматически созданный `Teams app manifest` с портала. Выполните следующие шаги перед проверкоц или публикацией приложения:

1. [Включение двух значков](../../concepts/build-and-test/apps-package.md#app-icons).
1. Измените раздел `icons` манифеста, чтобы включить имена файлов значков вместо URL-адресов.

Приведенный ниже файл manifest.json содержит элементы, необходимые для тестирования и отправки приложения.

> [!NOTE]
> Замените `id` и `connectorId` в приведенном ниже примере на глобальный уникальный ИД соединителя.

#### <a name="example-of-manifestjson-with-connector"></a>Пример manifest.json с соединителем

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "id": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
  "version": "1.0",
  "packageName": "com.sampleapp",
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

Чтобы протестировать соединитель, загрузите его в команду с любым другим приложением. Вы можете создать ZIP-пакет, используя файл манифеста из двух файлов значков и соединителей на панели инструментов разработчика, измененный, как указано в разделе [Включение соединителя в манифест](#include-the-connector-in-your-manifest).

После отправки приложения откройте список соединителей с любого канала. Прокрутите вниз, чтобы найти свое приложение в разделе **Отправленные**.

![Снимок экрана раздела отправленных приложений в диалоговом окне соединителя](~/assets/images/connectors/connector_dialog_uploaded.png)

> [!NOTE]
> Поток выполняется полностью в Microsoft Teams в качестве размещенной функции.

Чтобы убедиться, что действие `HttpPOST` работает правильно, [отправьте сообщения в свой соединитель](~/webhooks-and-connectors/how-to/connectors-using.md).

Следуйте [пошаговым инструкциям](../../sbs-teams-connectors.yml), чтобы создать и проверить соединители в Microsoft Teams.

## <a name="distribute-webhook-and-connector"></a>Распространение веб-перехватчика и соединителя

1. [Настройте входящий веб-перехватчик](~/webhooks-and-connectors/how-to/add-incoming-webhook.md#create-an-incoming-webhook) непосредственно для своей команды.

1. Добавьте [страницу конфигурации](~/webhooks-and-connectors/how-to/connectors-creating.md?#integrate-the-configuration-experience) и опубликуйте входящий веб-перехватчик в соединителе Office 365.

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
