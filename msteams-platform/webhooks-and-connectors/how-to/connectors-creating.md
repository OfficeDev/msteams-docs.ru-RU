---
title: Создание соединителей Office 365
author: laujan
description: Описывает, как начать работу с Office 365 соединители в Microsoft Teams
keywords: Соединитель Office 365 в Teams
ms.localizationpriority: medium
ms.topic: conceptual
ms.date: 06/16/2021
ms.openlocfilehash: 64400b3f80aa5ba322ce7318e0261e8b694e7e18
ms.sourcegitcommit: bfa9d24f736fb8915a9e3ef09c47dbe29a950cb5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/14/2022
ms.locfileid: "62801385"
---
# <a name="create-office-365-connectors"></a>Создание соединителей Office 365

С Microsoft Teams приложениями можно добавить существующие Office 365 соединителю или создать новый в Teams. Дополнительные сведения см. в [дополнительных сведениях о создании собственного соединитетеля](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector).

## <a name="add-a-connector-to-teams-app"></a>Добавление соединителю в Teams приложение

Вы можете создать пакет [и](~/concepts/build-and-test/apps-package.md) [опубликовать](~/concepts/deploy-and-publish/apps-publish.md) соединители в рамках отправки AppSource. Вы можете распространять зарегистрированный соединитатель как часть пакета Teams приложения. Сведения о точках входа для Teams приложения см. [в таблице capabilities](~/concepts/extensibility-points.md). Вы также можете предоставить пакет пользователям непосредственно для загрузки в Teams.

Чтобы распределить соединитело, зарегистрируйте его в панели мониторинга разработчиков [соединители](https://aka.ms/connectorsdashboard).

Чтобы соединители работали только в Microsoft Teams, следуйте инструкциям по отправке соединитетеля в публикации приложения в Microsoft Teams [магазине](~/concepts/deploy-and-publish/appsource/publish.md). В противном случае зарегистрированный соединитатель работает во всех Office 365, поддерживаюх приложения, включая Outlook и Teams.

> [!IMPORTANT]
> Соединитель регистрируется после выбора **сохранить** в панели мониторинга разработчика соединители. Если вы хотите опубликовать соединителе в AppSource, следуйте инструкциям в публикации [Microsoft Teams приложения в AppSource](~/concepts/deploy-and-publish/apps-publish.md). Если вы не хотите публиковать приложение в AppSource, раздайте его непосредственно организации. После [публикации соединители для организации](#publish-connectors-for-the-organization) никаких дополнительных действий на панели мониторинга соединители не требуется.

### <a name="integrate-the-configuration-experience"></a>Интеграция опытом настройки

Пользователи могут выполнить весь процесс настройки соединитетеля, не покидая Teams клиента. Чтобы получить опыт, Teams встраить страницу конфигурации непосредственно в iframe. Последовательность операций следующим образом:

1. Для начала процесса настройки пользователь выбирает соединител.
1. Пользователь взаимодействует с веб-интерфейсом для завершения конфигурации.
1. Пользователь выбирает **сохранить,** что вызывает вызов в коде.

    > [!NOTE]
    > * Код может обработать событие сохранения путем восстановления параметров веб-ок. Код хранит веб-сайт для публикации событий позже.
    > * В пределах Teams загружается Teams.

Вы можете повторно использовать существующие возможности веб-конфигурации или создать отдельную версию, которая будет организована в Teams. Код должен включать Microsoft Teams JavaScript SDK. Это дает коду доступ к API для выполнения общих операций, таких как получение текущего контекста пользователя, канала или группы и начало потоков проверки подлинности.

**Интеграция опытом конфигурации**

1. Инициализация SDK происходит путем вызова `microsoftTeams.initialize()`.
1. Вызов, `microsoftTeams.settings.setValidityState(true)` чтобы включить **сохранение**.

    > [!NOTE]
    > Вы должны вызвать в `microsoftTeams.settings.setValidityState(true)` качестве ответа на выбор пользователя или обновление поля.

1. Регистрируйте  `microsoftTeams.settings.registerOnSaveHandler()` обработник событий, который называется, когда пользователь выбирает **Сохранить**.
1. Вызов `microsoftTeams.settings.setSettings()` для сохранения параметров соединитетеля. Сохраненные параметры также показаны в диалоговом окне конфигурации, если пользователь пытается обновить существующую конфигурацию для соединитетеля.
1. Вызов `microsoftTeams.settings.getSettings()` для получения свойств веб-сайта, включая URL-адрес.

    > [!NOTE]
    > При первой `microsoftTeams.settings.getSettings()` загрузке страницы в случае перенастройки необходимо вызвать вызов.

1. Регистрируйте `microsoftTeams.settings.registerOnRemoveHandler()` обработчик событий, который называется, когда пользователь удаляет соединители.

Это событие предоставляет службе возможность выполнять любые действия по очистке.

В следующем коде содержится пример HTML для создания страницы конфигурации соединителя без обслуживания и поддержки клиентов:

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

Чтобы проверить подлинность пользователя в рамках загрузки страницы, см. поток [](~/tabs/how-to/authentication/auth-flow-tab.md) проверки подлинности для вкладки для интеграции в систему при вложении страницы.

> [!NOTE]
> В связи с перекрестной совместимостью клиента перед `microsoftTeams.authentication.registerAuthenticationHandlers()` вызовом код должен звонить с URL-адресом `authenticate()`и методами успешного или неудачного вызова.

#### <a name="getsettings-response-properties"></a>`GetSettings` Свойства ответа

>[!NOTE]
>Параметры, возвращенные `getSettings` вызовом, отличаются при вызове этого метода из вкладки и отличаются от параметров [js](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true).

В следующей таблице параметров и сведений о свойствах `GetSetting` отклика:

| Параметры   | Details |
|-------------|---------|
| `entityId`       | Код сущности, задаваемый кодом при вызове `setSettings()`. |
| `configName`  | Имя конфигурации, заданная кодом при вызове `setSettings()`. |
| `contentUrl` | URL-адрес страницы конфигурации, заданная кодом при вызове `setSettings()`. |
| `webhookUrl` | URL-адрес веб-страницы, созданный для соединителя. Для отправки карт на канал используйте URL-адрес веб-сайта POST, структурированный JSON. Возвращается `webhookUrl` только тогда, когда приложение возвращает данные успешно. |
| `appType` | Возвращаемые значения могут `mail`быть соответствующими `groups``teams` Office 365 mail, Office 365 группам или Microsoft Teams соответственно. |
| `userObjectId` | Уникальный ID, соответствующий Office 365, который инициировал настройка соединиттеля. Она должна быть защищена. Это значение можно использовать для связи пользователя в Office 365, который настроил конфигурацию в службе. |

#### <a name="handle-edits"></a>Обработка изменений

Код должен обрабатывать пользователей, которые возвращаются, чтобы изменить существующую конфигурацию соединитетеля. Для этого необходимо вызвать во `microsoftTeams.settings.setSettings()` время начальной конфигурации со следующими параметрами:

- `entityId` это пользовательский ID, который представляет то, что пользователь настроил и понял в вашей службе.
- `configName` это имя, которое код конфигурации может получить.
- `contentUrl` это настраиваемый URL-адрес, загружаемый при редактировании существующей конфигурации соединителя.

Этот вызов выполнен в рамках обработки событий сохранения. Затем при загрузке `contentUrl` `getSettings()` кода необходимо вызвать для предварительного заполнения любых параметров или форм в пользовательском интерфейсе конфигурации.

#### <a name="handle-removals"></a>Обработка удалений

Обработчик событий можно выполнить, если пользователь удаляет существующую конфигурацию соединитетеля. Этот обработок регистрируется по вызову `microsoftTeams.settings.registerOnRemoveHandler()`. Этот обработок используется для выполнения операций очистки, например для удаления записей из базы данных.

### <a name="include-the-connector-in-your-manifest"></a>Включите соединители в манифест

Скачайте авто, сгенерированную `Teams app manifest` с портала. Выполните следующие действия перед тестированием или публикацией приложения:

1. [Включение двух значков](../../concepts/build-and-test/apps-package.md#app-icons).
1. Измените `icons` часть манифеста, чтобы включить имена файлов значков вместо URL-адресов.

В следующем файле manifest.json содержатся элементы, необходимые для тестирования и отправки приложения:

> [!NOTE]
> Замените `id` `connectorId` и в следующем примере guID соединитетеля.

#### <a name="example-of-manifestjson-with-connector"></a>Пример manifest.json с соединитетелем

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

## <a name="enable-or-disable-connectors-in-teams"></a>Включить или отключить соединители в Teams

Модуль Exchange Online PowerShell V2 использует современную проверку подлинности и работает с многофакторной проверкой подлинности под названием MFA для подключения Exchange связанных сред PowerShell в Microsoft 365. Администраторы могут использовать Exchange Online PowerShell для отключения соединители для всего клиента или определенного почтового ящика группы, затрагивая всех пользователей в этом клиенте или почтовом ящике. Отключение для одних и не для других невозможно. Кроме того, соединители отключены по умолчанию для облако сообщества для государственных организаций, называемых GCC клиентов.

Параметр уровня клиента переопределяет параметр группового уровня. Например, если администратор включает соединители для группы и отключает их в клиенте, соединители для группы отключены. Чтобы включить соединитель в Teams, подключите Exchange Online [PowerShell](/powershell/exchange/connect-to-exchange-online-powershell?view=exchange-ps#connect-to-exchange-online-powershell-using-modern-authentication-with-or-without-mfa&preserve-view=true) с помощью современной проверки подлинности с помощью MFA или без него.

### <a name="commands-to-enable-or-disable-connectors"></a>Команды, позволяющие включить или отключить соединители

В Exchange Online PowerShell выполните следующие команды.

* Отключение соединители для клиента: `Set-OrganizationConfig -ConnectorsEnabled:$false`.
* Отключение действий для клиента: `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$false`.
* Чтобы включить соединители для Teams, запустите следующие команды:
  * `Set-OrganizationConfig -ConnectorsEnabled:$true `
  * `Set-OrganizationConfig -ConnectorsEnabledForTeams:$true`
  * `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$true`

Дополнительные сведения об обмене модулями PowerShell см. в [обзоре Set-OrganizationConfig](/powershell/module/exchange/Set-OrganizationConfig?view=exchange-ps&preserve-view=true). Чтобы включить или отключить Outlook соединители, [подключите приложения к](https://support.microsoft.com/topic/connect-apps-to-your-groups-in-outlook-ed0ce547-038f-4902-b9b3-9e518ae6fbab?ui=en-us&rs=en-us&ad=us) группам в Outlook.

## <a name="test-your-connector"></a>Тестирование соединитетеля

Чтобы проверить соединители, загрузите его в команду с любым другим приложением. Вы можете создать пакет .zip с помощью файла манифеста из двух файлов значков и соединителов Панели мониторинга разработчика, измененных как указано в Включите соединитетель в [манифесте](#include-the-connector-in-your-manifest).

После отправки приложения откройте список соединитений из любого канала. Прокрутите вниз, чтобы просмотреть приложение в разделе **Uploaded** :

![Снимок экрана загруженного раздела в диалоговом окне соединитель](~/assets/images/connectors/connector_dialog_uploaded.png)

> [!NOTE]
> Поток происходит полностью в пределах Microsoft Teams в качестве хозяйского опыта.

Чтобы убедиться, `HttpPOST` что действие работает правильно, [отправьте сообщения в соединителю](~/webhooks-and-connectors/how-to/connectors-using.md).

## <a name="publish-connectors-for-the-organization"></a>Публикация соединители для организации

Если вы хотите, чтобы соединители были доступны только пользователям в организации, вы можете загрузить свое настраиваемое приложение соединители в каталог [приложений организации](~/concepts/deploy-and-publish/apps-publish.md).

После отправки пакета приложений для настройки и использования соединителя в команде установите соединители из каталога приложений организации.

**Настройка соединитетеля**

1. Выберите **Приложения** из левой панели навигации.
1. В разделе **Приложения** выберите **соединители**.
1. Выберите соединителю, который необходимо добавить. Появляется всплывающее диалоговое окно.
1. В меню dropdown выберите **Добавить в команду**.
1. В поле поиска введите команду или имя канала.
1. Выберите **Настройка соединителя из** выпадаемого меню в правом нижнем углу окна диалогов.

> [!IMPORTANT]
> В настоящее время настраиваемые соединители недоступны в облако сообщества для государственных организаций (GCC), GCC-High и Department of Defense (DoD).

Соединитель доступен в разделе &#9679;&#9679;&#9679; > **OptionsConnectorsAllConnectors** >  >  >  **для вашей** команды. Вы можете перемещаться путем прокрутки в этот раздел или поиска соединитеного приложения. Чтобы настроить или изменить соединители, выберите **Настройка**.

## <a name="distribute-webhook-and-connector"></a>Распространение веб-ок и соединители

1. [Настройка входящих веб-ок непосредственно](~/webhooks-and-connectors/how-to/add-incoming-webhook.md?branch=pr-en-us-3076#create-incoming-webhook) для вашей команды.
1. Добавьте [страницу конфигурации](~/webhooks-and-connectors/how-to/connectors-creating.md?branch=pr-en-us-3076#integrate-the-configuration-experience) [и опубликуйте](~/webhooks-and-connectors/how-to/connectors-creating.md?branch=pr-en-us-3076#publish-connectors-for-the-organization) входящий веб-сайт в Office 365 соединителю.
1. Пакет и публикация соединитетеля в рамках отправки [AppSource](~/concepts/deploy-and-publish/office-store-guidance.md) .

## <a name="code-sample"></a>Пример кода

В следующей таблице приводится пример имени и его описания:

|**Название примера** | **Описание** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| Connectors    | Пример Office 365 соединители, генерирующие уведомления для Teams канала.|   [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-todo-notification/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-github-notification/nodejs)|
| Общий пример соединители |Пример кода для общего соединители, который легко настроить для любой системы, поддерживающую веб-сайты.|  | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-generic/nodejs)|

## <a name="see-also"></a>Дополнительные ресурсы

* [Создание и отправка сообщений](~/webhooks-and-connectors/how-to/connectors-using.md)
* [Создание входящего веб-перехватчика](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [Создание соединителя Office 365](~/webhooks-and-connectors/how-to/connectors-creating.md)
