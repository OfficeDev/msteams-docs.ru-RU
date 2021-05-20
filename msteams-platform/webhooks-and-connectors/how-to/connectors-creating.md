---
title: Соединители Office 365
description: Описывает, как начать работу с Office 365 разъемами в Microsoft Teams
keywords: соединитель teams o365
localization_priority: Normal
ms.topic: conceptual
ms.date: 04/19/2019
ms.openlocfilehash: 9eaaedf88d907dd7a7422068ab5d20450345f0e7
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566812"
---
# <a name="creating-office-365-connectors-for-microsoft-teams"></a>Создание Office 365 разъемов для Microsoft Teams

>С Microsoft Teams приложениями вы можете добавить существующий Office 365 Connector или построить новый, который будет включен в Microsoft Teams. Для [получения дополнительной информации смотрите создать](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) свой собственный разъем.

## <a name="adding-a-connector-to-your-teams-app"></a>Добавление разъема в приложение Teams приложение

Зарегистрированный соединитель можно распространять в составе пакета приложений Teams. Будь то автономное решение или [](~/concepts/extensibility-points.md) одна из нескольких возможностей, которые позволяет ваш опыт в Teams, [вы](~/concepts/build-and-test/apps-package.md) можете упаковать и [опубликовать](~/concepts/deploy-and-publish/apps-publish.md) ваш разъем как часть вашего представления AppSource, или вы можете предоставить его пользователям непосредственно для загрузки в течение Teams.

Для распространения разъема необходимо зарегистрироваться с помощью панели [разработчиков Connectors.](https://outlook.office.com/connectors/home/login/#/publish) По умолчанию, после регистрации Коннектора, предполагается, что ваш разъем будет работать во всех Office 365 продуктах, которые их поддерживают, включая Outlook и Teams. Если это _не так,_ и вам нужно создать разъем, который работает только в Microsoft Teams, свяжитесь с [нами непосредственно Microsoft Teams App Представлений](mailto:teamsubm@microsoft.com).

> [!IMPORTANT]
> После выбора **Save in** the Connectors Developer Dashboard ваш разъем регистрируется. Если вы хотите опубликовать свой разъем в AppSource, следуйте инструкциям [в Publish your Microsoft Teams приложение AppSource](~/concepts/deploy-and-publish/apps-publish.md). Если вы не хотите публиковать свое приложение в AppSource, а просто распространять его только среди вашей организации, вы можете сделать это, [опубликовав в вашей организации.](#publish-connectors-for-your-organization) Если вы хотите опубликовать информацию только в организации, никаких дальнейших действий на панели мониторинга Connector не требуется.

### <a name="integrating-the-configuration-experience"></a>Интеграция опыта конфигурации

Пользователи заверят весь процесс настройки Connector, не покидая Teams клиента. Для достижения этой цели Teams встраивает страницу конфигурации непосредственно в iframe. Последовательность операций заключается в следующем:

1. Пользователь нажимает на разъем, чтобы начать процесс настройки.
2. Teams загрузит ваш опыт конфигурации в соответствии.
3. Пользователь взаимодействует с веб-интерфейсом для завершения конфигурации.
4. Пользователь нажимает "Сохранить", который вызывает обратный вызов в коде.
5. Ваш код обработать событие сохранения путем извлечения параметров webhook (описано ниже). Ваш код должен хранить webhook для поста событий позже.

Вы можете повторно использовать существующий веб-конфигурации опыт или создать отдельную версию, которая будет размещена специально в Teams. Ваш код должен:

1. Включите Microsoft Teams JavaScript SDK. Это дает коду доступ к API для выполнения общих операций, таких как получение текущего контекста пользователя/канала/команды и инициирование потоков аутентификации. Инициализация SDK происходит путем вызова `microsoftTeams.initialize()`.
2. `microsoftTeams.settings.setValidityState(true)`Звоните, когда хотите включить кнопку Сохранения. Вы должны сделать это в ответ на действительный пользовательский ввод, например, выбор или обновление поля.
3. Зарегистрируйте обработчик `microsoftTeams.settings.registerOnSaveHandler()` событий, который вызывается при нажатии кнопки Save.
4. `microsoftTeams.settings.setSettings()`Звоните, чтобы сохранить настройки разъема. Здесь также сохраняется то, что будет показано в диалоге конфигурации, если пользователь попытается обновить существующую конфигурацию для вашего разъема.
5. `microsoftTeams.settings.getSettings()`Звоните, чтобы получить свойства webhook, включая сам URL. Вы должны позвонить по этому вопросу В дополнение к событию сохранения, вы также должны позвонить по этому вопросу, когда ваша страница впервые загружена в случае повторной конфигурации.
6. (По желанию) Зарегистрируйте обработчик `microsoftTeams.settings.registerOnRemoveHandler()` событий, который вызывается, когда пользователь удаляет ваш разъем. Это событие дает вашему сервису возможность выполнять любые действия по очистке.

Вот пример HTML для создания страницы конфигурации Connector без CSS:

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

#### <a name="getsettings-response-properties"></a>`GetSettings()` свойства ответа

>[!Note]
>Параметры, возвращенные вызовом `getSettings` здесь, отличаются от тех, которые вы должны были вызвать этот метод из вкладки, и отличаются от тех, которые описаны [здесь.](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true)

| Параметр   | Сведения |
|-------------|---------|
| `entityId`       | Идентификатор сущности, установленный кодом при `setSettings()` вызове. |
| `configName`  | Имя конфигурации, как установлено кодом при `setSettings()` вызове. |
| `contentUrl` | URL страницы конфигурации, установленный кодом при `setSettings()` вызове. |
| `webhookUrl` | URL webhook, созданный для этого разъема. Упорствуй webhook URL и использовать его для POST структурированных JSON для отправки карт на канал. Параметр `webhookUrl` возвращается только в том случае, если приложение возвращается успешно. |
| `appType` | Возвращаемыми значениями могут быть `mail`, `groups` или `teams` (для почты Office 365, функции "Группы Office 365" и Microsoft Teams соответственно). |
| `userObjectId` | Это уникальный идентификатор, соответствующий Office 365, инициировавший настройку разъема. Этот параметр должен быть защищен. Это значение используется для сопоставления пользователя в Office 365, который настраивает конфигурацию, и пользователя в вашей службе. |

Если вам необходимо проверить подлинность пользователя в рамках загрузки страницы в шаге 2 выше, обратитесь к этой ссылке для [получения подробной](~/tabs/how-to/authentication/auth-flow-tab.md) информации о том, как вы можете интегрировать логин, когда ваша страница встроена.

> [!NOTE]
> По причинам совместимости между клиентами, ваш код должен будет позвонить с URL и `microsoftTeams.authentication.registerAuthenticationHandlers()` методы возврата вызова успеха/неудачи перед вызовом. `authenticate()`

#### <a name="handling-edits"></a>Обработка правок

Код должен обрабатывать пользователей, возвращающихся для изменения существующей конфигурации соединителя. Для этого вызов в `microsoftTeams.settings.setSettings()` течение начальной конфигурации со следующими параметрами:

- `entityId` это пользовательский идентификатор, который понимается вашим сервисом и представляет то, что пользователь настроил.
- `configName` это дружелюбное имя, которое код конфигурации может получить
- `contentUrl` это пользовательский URL-адрес, который загружается, когда пользователь редактирует существующую конфигурацию разъема. Вы можете использовать этот URL, чтобы облегчить обработку кода в случае редактирования.

Как правило, этот вызов делается как часть обработчика событий сохранения. Затем, когда `contentUrl` вышеуказанное загружено, код должен вызвать для `getSettings()` преднаселения любые настройки или формы в пользовательском интерфейсе конфигурации.

#### <a name="handling-removals"></a>Обработка удалений

Вы можете дополнительно выполнить обработчик событий, когда пользователь удаляет существующую конфигурацию разъема. Вы регистрируете этот обработчик по телефону `microsoftTeams.settings.registerOnRemoveHandler()` . Этот обработчик может быть использован для выполнения операций по очистке, таких как удаление записей из базы данных.

### <a name="including-the-connector-in-your-manifest"></a>Включение разъема в манифест

Вы можете скачать автоматически сгенерированный Teams манифест приложения с портала. Однако, прежде чем использовать его для тестирования или публикации приложения, необходимо сделать следующее:

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

## <a name="testing-your-connector"></a>Тестирование соединителя

Чтобы тестировать соединитель, отправьте его команде, как в любом другом приложении. Вы можете создать ZIP-пакет, используя файл манифеста с панели администрирования для разработчиков соединителей (измененный согласно инструкциям из предыдущего раздела) и два файла значков.

После отправки приложения откройте список соединителей с любого канала. Прокрутите вниз, чтобы найти свое приложение в разделе **Отправленные**.

![Снимок экрана раздела отправленных приложений в диалоговом окне соединителя](~/assets/images/connectors/connector_dialog_uploaded.png)

Теперь можно запустить среду настройки. Имейте в виду, что этот поток происходит Microsoft Teams в качестве размещены опыт.

Чтобы убедиться, `HttpPOST` что действие работает правильно, отправьте сообщения в [разъем.](~/webhooks-and-connectors/how-to/connectors-using.md)

## <a name="publish-connectors-for-your-organization"></a>Публикация разъемов для вашей организации

Иногда вы можете не публиковать приложение-разъем для общедоступных AppSource/Store, но хотели бы, чтобы оно было доступно только пользователям в вашей организации. В таких случаях вы можете загрузить пользовательское приложение-разъем в [каталог приложений вашей организации.](~/concepts/deploy-and-publish/apps-publish.md) Таким образом, ваше приложение-разъем будет доступно только этой организации, и вам не нужно будет публиковать свой разъем в общедоступный магазин.

После загрузки пакета приложений для настройки и использования разъема в команде он может быть установлен из каталога приложений организации, следуя следующим шагам:

1. Выберите значок приложений из крайне левой вертикальной навигационной полосы.
1. В окне **Приложения** выберите **разъемы.**
1. Выберите разъем, который вы хотите добавить, и всплывающее окно диалога будет отображаться.
1. Выберите **добавить в бар** команды.
1. В следующем диалоговом окне ввемите имя команды или канала.
1. Выберите **стойку разъема** из правого нижнего угла окна диалога.
1. Разъем будет доступен в разделе, &#9679;&#9679;&#9679; и> *больше*  =>  *вариантов*  =>  *Разъемы*  =>  *Все разъемы для вас команда* для этой команды. Вы можете перемещаться, прокручивая в этот раздел или искать разъем приложения.
1. Для настройки или изменения разъема выберите **планку Configure.**

## <a name="code-sample"></a>Пример кода
|**Название образца** | **Описание** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| Соединители    | Пример Office 365 Connector, генерирующий уведомления для команд канала.|   [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-todo-notification/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-github-notification/nodejs)|
| Общий образец разъемов |Пример кода для общего разъема, который легко настроить для любой системы, которая поддерживает webhooks.|  | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-generic/nodejs)|
