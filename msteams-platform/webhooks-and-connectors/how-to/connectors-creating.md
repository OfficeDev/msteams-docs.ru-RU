---
title: Соединители Office 365
description: Описывает, как начать работу с Office 365 соединители в Microsoft Teams
keywords: соединитель teams o365
localization_priority: Normal
ms.topic: conceptual
ms.date: 04/19/2019
ms.openlocfilehash: ace546853d7dfe9773055288a0fc3471fe656652
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2021
ms.locfileid: "52629825"
---
# <a name="creating-office-365-connectors-for-microsoft-teams"></a>Создание Office 365 соединители для Microsoft Teams

С Microsoft Teams приложениями можно добавить существующие Office 365 соединителю или создать новый, чтобы включить Microsoft Teams. Дополнительные [сведения см. в "Сборке](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) собственного соединитетеля".

## <a name="adding-a-connector-to-your-teams-app"></a>Добавление соединитетеля в Teams App

Зарегистрированный соединитель можно распространять в составе пакета приложений Teams. Независимо от того, является ли это автономным решением или одним из нескольких [](~/concepts/build-and-test/apps-package.md) возможностей, [](~/concepts/deploy-and-publish/apps-publish.md) которые вы можете использовать в Teams, вы можете упаковать и опубликовать соединитель в составе отправки AppSource или предоставить его пользователям непосредственно для загрузки в Teams. [](~/concepts/extensibility-points.md)

Для распространения соединитетеля необходимо зарегистрироваться с помощью панели мониторинга разработчиков [соединители.](https://outlook.office.com/connectors/home/login/#/publish) По умолчанию после регистрации соединительщика предполагается, что соединительщик будет работать во всех продуктах Office 365, которые их поддерживают, включая Outlook и Teams. Если это _не_ так, и вам нужно создать соединителя, который работает только в Microsoft Teams, свяжитесь с нами непосредственно в Microsoft Teams [отправки приложений](mailto:teamsubm@microsoft.com).

> [!IMPORTANT]
> После выбора **сохранить в** панели мониторинга разработчиков соединители, соединитель зарегистрирован. Если вы хотите опубликовать свой соединититель в AppSource, следуйте инструкциям в [Публикации Microsoft Teams приложения в AppSource](~/concepts/deploy-and-publish/apps-publish.md). Если вы не хотите публиковать свое приложение в AppSource, а просто распространять его только в организации, вы можете сделать это, опубликовав [в организации](#publish-connectors-for-your-organization). Если требуется только опубликовать в организации, никаких дополнительных действий на панели мониторинга Connector не требуется.

### <a name="integrating-the-configuration-experience"></a>Интеграция работы с конфигурацией

Пользователи завершят весь процесс настройки соединители, не покидая Teams клиента. Чтобы добиться этого, Teams встраит страницу конфигурации непосредственно в iframe. Последовательность операций следующим образом:

1. Пользователь щелкает соединитетелем, чтобы начать процесс настройки.
2. Teams загрузит ваш опыт настройки в строку.
3. Пользователь взаимодействует с веб-интерфейсом для завершения конфигурации.
4. Пользователь нажимает кнопку "Сохранить", которая вызывает вызов в коде.
5. Код обработать событие сохранения путем восстановления параметров веб-ок (описано ниже). Затем код должен хранить веб-сайт для публикации событий позже.

Вы можете повторно использовать существующие возможности веб-конфигурации или создать отдельную версию, которая будет организована в Teams. Код должен:

1. Включай Microsoft Teams JavaScript SDK. Это дает коду доступ к API для выполнения общих операций, таких как получение текущего контекста пользователя/канала или группы и начало потоков проверки подлинности. Инициализация SDK происходит путем вызова `microsoftTeams.initialize()`.
2. Вызов, `microsoftTeams.settings.setValidityState(true)` когда необходимо включить кнопку Сохранить. Это необходимо сделать в качестве ответа на допустимые входные данные пользователей, такие как выбор или обновление поля.
3. Зарегистрируйте `microsoftTeams.settings.registerOnSaveHandler()` обработник событий, который будет вызван при нажатии пользователем кнопки Сохранить.
4. Вызов `microsoftTeams.settings.setSettings()` для сохранения параметров соединитетеля. Сохранено также то, что будет показано в диалоговом окне конфигурации, если пользователь попытается обновить существующую конфигурацию для соединитетеля.
5. Вызов `microsoftTeams.settings.getSettings()` для получения свойств webhook, включая сам URL-адрес. Вы должны вызвать это в дополнение к во время события сохранения, вы также должны вызвать это, когда ваша страница впервые загружена в случае повторной настройки.
6. (Необязательный) Зарегистрируйте `microsoftTeams.settings.registerOnRemoveHandler()` обработчик событий, который будет вызван после удаления соединитетелем пользователя. Это событие предоставляет службе возможность выполнять любые действия по очистке.

Вот пример HTML для создания страницы конфигурации соединителя без CSS:

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

#### <a name="getsettings-response-properties"></a>`GetSettings()` Свойства ответа

>[!Note]
>Параметры, возвращенные здесь вызовом, отличаются от тех, которые вы должны были вызвать этот метод со вкладки, и отличаются от параметров, задокументированных `getSettings` [здесь.](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)

| Параметр   | Сведения |
|-------------|---------|
| `entityId`       | Код сущности, задаваемый кодом при `setSettings()` вызове. |
| `configName`  | Имя конфигурации, заданная кодом при `setSettings()` вызове. |
| `contentUrl` | URL-адрес страницы конфигурации, заданная кодом при `setSettings()` вызове. |
| `webhookUrl` | URL-адрес веб-страницы, созданный для этого соединителя. Сохраните URL-адрес веб-страницы и используйте его в структуре POST JSON для отправки карт на канал. Параметр `webhookUrl` возвращается только в том случае, если приложение возвращается успешно. |
| `appType` | Возвращаемыми значениями могут быть `mail`, `groups` или `teams` (для почты Office 365, функции "Группы Office 365" и Microsoft Teams соответственно). |
| `userObjectId` | Это уникальный id, соответствующий Office 365, который инициировал установку соединиттеля. Этот параметр должен быть защищен. Это значение используется для сопоставления пользователя в Office 365, который настраивает конфигурацию, и пользователя в вашей службе. |

Если необходимо проверить подлинность пользователя в рамках загрузки страницы на шаге 2 выше, обратитесь к этой ссылке, чтобы узнать, как интегрировать вход при вложении страницы. [](~/tabs/how-to/authentication/auth-flow-tab.md)

> [!NOTE]
> В связи с причинами совместимости между клиентами перед вызовом коду необходимо звонить с помощью URL-адреса и методов вызова успешного `microsoftTeams.authentication.registerAuthenticationHandlers()` и неудачного `authenticate()` вызова.

#### <a name="handling-edits"></a>Обработка изменений

Код должен обрабатывать пользователей, возвращающихся для изменения существующей конфигурации соединителя. Для этого необходимо вызвать `microsoftTeams.settings.setSettings()` во время начальной конфигурации со следующими параметрами:

- `entityId` это пользовательский ID, который понимается службой и представляет то, что пользователь настроил.
- `configName` это удобное имя, которое код конфигурации может получить
- `contentUrl` это настраиваемый URL-адрес, загружаемый при редактировании существующей конфигурации соединителя. Этот URL-адрес можно использовать, чтобы упростить обработку дела редактирования для кода.

Как правило, этот вызов проводится в рамках обработки событий сохранения. Затем при загрузке кода должен вызываться предварительная загрузка параметров или форм в пользовательском интерфейсе `contentUrl` `getSettings()` конфигурации.

#### <a name="handling-removals"></a>Обработка удалений

Обработчик событий можно выполнить, если пользователь удаляет существующую конфигурацию соединителю. Этот обработок регистрируется по вызову `microsoftTeams.settings.registerOnRemoveHandler()` . Этот обработок можно использовать для выполнения операций очистки, таких как удаление записей из базы данных.

### <a name="including-the-connector-in-your-manifest"></a>В том числе соединители в манифесте

Вы можете скачать автогенерированную Teams с портала. Однако прежде чем использовать его для тестирования или публикации приложения, необходимо сделать следующее:

- [Включение двух значков](../../concepts/build-and-test/apps-package.md#app-icons).
- Измените раздел `icons` манифеста, чтобы он ссылался на имена файлов значков, а не на их URL-адреса.

Приведенный ниже файл manifest.json содержит основные элементы, необходимые для тестирования и отправки приложения.

> [!NOTE]
> Замените `id` и `connectorId` в приведенном ниже примере на GUID соединителя.

#### <a name="example-manifestjson-with-connector"></a>Пример файла manifest.json с соединителем

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
    "full": "This is a sample manifest for an app with a connector with an inline configuration experience.",
    "short": "This is a sample manifest for an app with a connector."
  },
  "icons": {
    "outline": "sampleapp-outline.png",
    "color": "sampleapp-color.png"
  },
  "connectors": [
    {
      "connectorId": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
      "configurationUrl": "https://teamstodoappconnectorwithinlineconfig.azurewebsites.net/Connector/Setup",
      "scopes": [
        "team"
      ]
    }
  ],
  "name": {
    "short": "Sample App",
    "full": "Sample App Long Name"
  },
  "accentColor": "#FFFFFF"
}
```

## <a name="disable-or-enable-connectors-in-teams"></a>Отключить или включить соединители в Teams

Модуль Exchange Online PowerShell V2 использует современную проверку подлинности и работает с многофакторной проверкой подлинности (MFA) для подключения Exchange связанных с powerShell сред в Microsoft 365. Администраторы могут использовать Exchange Online PowerShell для отключения соединители для всего клиента или определенного почтового ящика группы, затрагивая всех пользователей в этом клиенте или почтовом ящике. Отключение для одних и не для других невозможно. Кроме того, соединители отключены по умолчанию для GCC клиентов.

Параметр на уровне клиента переопределяет параметр группового уровня. Например, если администратор включает соединители для группы и отключает их в клиенте, соединители для группы будут отключены. Чтобы включить соединитель в Teams, подключите Exchange Online [PowerShell](/docs.microsoft.com/powershell/exchange/connect-to-exchange-online-powershell?view=exchange-ps#connect-to-exchange-online-powershell-using-modern-authentication-with-or-without-mfa&preserve-view=true) с помощью современной проверки подлинности с помощью MFA или без него.

### <a name="commands-to-disable-or-enable-connectors"></a>Команды по отключению или включении соединители

**Запустите команду в Exchange Online PowerShell**

* Отключение соединители для клиента: `Set-OrganizationConfig -ConnectorsEnabled:$false` .
* Отключение действий для клиента: `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$false` .
* Чтобы включить соединители для Teams, запустите следующие команды:
    * `Set-OrganizationConfig -ConnectorsEnabled:$true `
    * `Set-OrganizationConfig -ConnectorsEnabledForTeams:$true`
    * `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$true`

Дополнительные сведения об обмене модулями PowerShell см. в [сайте Set-OrganizationConfig.](/docs.microsoft.com/powershell/module/exchange/Set-OrganizationConfig.md?view=exchange-ps&preserve-view=true) Чтобы включить или отключить Outlook соединители, [подключите приложения к](https://support.microsoft.com/topic/connect-apps-to-your-groups-in-outlook-ed0ce547-038f-4902-b9b3-9e518ae6fbab?ui=en-us&rs=en-us&ad=us)группам в Outlook.

## <a name="testing-your-connector"></a>Тестирование соединителя

Чтобы тестировать соединитель, отправьте его команде, как в любом другом приложении. Вы можете создать ZIP-пакет, используя файл манифеста с панели администрирования для разработчиков соединителей (измененный согласно инструкциям из предыдущего раздела) и два файла значков.

После отправки приложения откройте список соединителей с любого канала. Прокрутите вниз, чтобы найти свое приложение в разделе **Отправленные**.

![Снимок экрана раздела отправленных приложений в диалоговом окне соединителя](~/assets/images/connectors/connector_dialog_uploaded.png)

Теперь можно запустить среду настройки. Следует помнить, что этот поток происходит полностью в Microsoft Teams в качестве хозяйского опыта.

Чтобы убедиться, `HttpPOST` что действие работает правильно, отправьте сообщения в [соединителю.](~/webhooks-and-connectors/how-to/connectors-using.md)

## <a name="publish-connectors-for-your-organization"></a>Публикация соединители для организации

Иногда может не потребоваться публиковать приложение соединители в общедоступный AppSource/Store, но вы хотите, чтобы оно было доступно только пользователям в вашей организации. В таких случаях вы можете загрузить свое настраиваемое соединитеное приложение в каталог [приложений вашей организации.](~/concepts/deploy-and-publish/apps-publish.md) Таким образом, приложение соединители будет доступно только этой организации, и вам не потребуется публиковать соединители в общедоступный магазин.

После загрузки пакета приложений для настройки и использования соединители в команде его можно установить из каталога приложений организации, следуя следующим шагам:

1. Выберите значок приложений из левой панели вертикальной навигации.
1. В **окне Приложения** выберите **соединители**.
1. Выберите соединителю, который необходимо добавить, и будет отображаться всплывающее диалоговое окно.
1. Выберите **добавить в планку команды.**
1. В следующем диалоговом окне введите команду или имя канала.
1. Выберите **строку Настройка соединитетеля** в правом нижнем углу окна диалогов.
1. Соединители будут доступны в разделе &#9679;&#9679;&#9679; => дополнительные параметры Соединители Все соединители для вас  =>    =>    =>  *команда* для этой группы. Вы можете перемещаться путем прокрутки в этот раздел или поиска соединитеного приложения.
1. Чтобы настроить или изменить соединители, выберите **планку Configure.**

## <a name="code-sample"></a>Пример кода
|**Пример имени** | **Описание** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| Соединители    | Пример Office 365 соединители, генерирующие уведомления для канала teams.|   [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-todo-notification/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-github-notification/nodejs)|
| Общий пример соединители |Пример кода для общего соединители, который легко настроить для любой системы, поддерживающую веб-сайты.|  | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-generic/nodejs)|
