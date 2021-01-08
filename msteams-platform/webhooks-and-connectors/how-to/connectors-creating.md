---
title: Соединители Office 365
description: Описание начала работы с соединитетелями Office 365 в Microsoft Teams
keywords: соединитель teams o365
ms.topic: conceptual
ms.date: 04/19/2019
ms.openlocfilehash: 62a27e8f7b218491682ff0b9216e428f51264d0a
ms.sourcegitcommit: 5f1d6c12d80d48f403b73586f68bacf15785c855
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/30/2020
ms.locfileid: "49739051"
---
# <a name="creating-office-365-connectors-for-microsoft-teams"></a>Создание соединители Office 365 для Microsoft Teams

>С помощью приложений Microsoft Teams вы можете добавить существующий соединителю Office 365 или создать новый, чтобы включить его в Microsoft Teams. Дополнительные [сведения см.](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) в подключении "Создание собственного соединитела".

## <a name="adding-a-connector-to-your-teams-app"></a>Добавление соединители в приложение Teams

Вы можете распространять зарегистрированный соединитатель в составе пакета приложения Teams. Независимо от того, является ли приложение автономным решением или одной из [](~/concepts/build-and-test/apps-package.md) нескольких [](~/concepts/deploy-and-publish/apps-publish.md) возможностей Teams, вы можете упаковать и опубликовать соединитель в составе отправки в AppSource или предоставить его пользователям непосредственно для отправки в Teams. [](~/concepts/extensibility-points.md)

Чтобы распространять соединители, необходимо зарегистрироваться с помощью панели мониторинга [разработчика соединитеителей.](https://outlook.office.com/connectors/home/login/#/publish) По умолчанию после регистрации соединитела предполагается, что он будет работать во всех продуктах Office 365, которые их поддерживают, включая Outlook и Teams. Если это _не так_ и вам нужно создать соединителя, который работает только в Microsoft Teams, свяжитесь с нами непосредственно на веб-сайте "Отправки приложений Microsoft [Teams".](mailto:teamsubm@microsoft.com)

> [!IMPORTANT]
> После выбора **"Сохранить"** в информационной панели разработчика соединитеителей соединитель будет зарегистрирован. Если вы хотите опубликовать соединители в AppSource, следуйте инструкциям в публикации приложения [Microsoft Teams в AppSource.](~/concepts/deploy-and-publish/apps-publish.md) Если вы не хотите публиковать приложение в AppSource, а просто распространяете его непосредственно в вашей организации, это можно сделать, опубликуя приложение [в своей организации.](#publish-connectors-for-your-organization) Если вы хотите опубликовать только в своей организации, никаких дополнительных действий на панели мониторинга соединители не требуется.

### <a name="integrating-the-configuration-experience"></a>Интеграция работы с конфигурацией

Пользователи будут полностью работать с конфигурацией соединители, не покидая клиент Teams. Для этого Teams встраит страницу конфигурации непосредственно в iframe. Последовательность операций:

1. Чтобы начать процесс настройки, пользователь щелкает соединители.
2. Teams загрузит ваш опыт настройки в строке.
3. Пользователь взаимодействует с веб-интерфейсом для завершения настройки.
4. Пользователь нажал кнопку "Сохранить", что вызывает в коде вызов.
5. Код обрабатывает событие сохранения, искомые параметры веб-hook (задокументированы ниже). Затем в коде должен храниться веб-сайт для публикации событий позже.

Вы можете повторно использовать существующие возможности веб-конфигурации или создать отдельную версию, которая будет предназначена специально для Teams. Код должен:

1. Включит в него SDK JavaScript для Microsoft Teams. Это дает коду доступ к API для выполнения распространенных операций, таких как получение текущего контекста пользователя, канала или группы и инициирование потоков проверки подлинности. Инициализировать SDK с помощью `microsoftTeams.initialize()` вызова.
2. Вызовите `microsoftTeams.settings.setValidityState(true)` этот вызов, если нужно включить кнопку "Сохранить". Это следует сделать в ответ на допустимые данные пользователя, такие как выбор или обновление поля.
3. `microsoftTeams.settings.registerOnSaveHandler()`Зарегистрируйте обработок событий, который будет вызван, когда пользователь нажмет кнопку "Сохранить".
4. Вызов `microsoftTeams.settings.setSettings()` для сохранения параметров соединители. Здесь также будет показано, что будет показано в диалоговом окне конфигурации, если пользователь попытается обновить существующую конфигурацию для соединители.
5. Вызов `microsoftTeams.settings.getSettings()` для получения свойств веб-hook, включая сам URL-адрес. Этот вызов следует вызывать не только во время события сохранения, но и при первой загрузке страницы при повторной настройке.
6. (Необязательно) `microsoftTeams.settings.registerOnRemoveHandler()` Зарегистрируйте обработчик событий, который будет вызван, когда пользователь удалит соединитер. Это событие предоставляет службе возможность выполнять любые действия по очистке.

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
            var removeCalled = true;
            alert("Removed" + JSON.stringify(removeEvent));
        });

</script>
```

#### <a name="getsettings-response-properties"></a>`GetSettings()` свойства ответа

>[!Note]
>Параметры, возвращенные здесь вызовом, отличаются от параметров, которые были бы вызваны этим методом на вкладке, и отличаются от параметров, задокументированных `getSettings` [здесь.](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true)

| Параметр   | Сведения |
|-------------|---------|
| `entityId`       | ИД сущности, задаваемой кодом при `setSettings()` вызове. |
| `configName`  | Имя конфигурации, заданная кодом при `setSettings()` вызове. |
| `contentUrl` | URL-адрес страницы конфигурации, заданная кодом при вызове `setSettings()` |
| `webhookUrl` | URL-адрес веб-hook, созданный для этого соединителя. Сохраните URL-адрес веб-hook и используйте его в post структурированной JSON для отправки карточек в канал. Параметр `webhookUrl` возвращается только в том случае, если приложение возвращается успешно. |
| `appType` | Возвращаемыми значениями могут быть `mail`, `groups` или `teams` (для почты Office 365, функции "Группы Office 365" и Microsoft Teams соответственно). |
| `userObjectId` | Это уникальный ид, соответствующий пользователю Office 365, который инициировал настройку соединители. Этот параметр должен быть защищен. Это значение используется для сопоставления пользователя в Office 365, который настраивает конфигурацию, и пользователя в вашей службе. |

Если вам нужно проверить подлинность пользователя при загрузке страницы на шаге 2 выше, обратитесь к этой ссылке, чтобы получить подробные сведения о том, как интегрировать вход при внедрении страницы. [](~/tabs/how-to/authentication/auth-flow-tab.md)

> [!NOTE]
> В связи с причинами совместимости между клиентами код должен будет вызываться с URL-адресом и методами успешного или неудачного вызова. `microsoftTeams.authentication.registerAuthenticationHandlers()` `authenticate()`

#### <a name="handling-edits"></a>Обработка изменений

Код должен обрабатывать пользователей, возвращающихся для изменения существующей конфигурации соединители. Для этого вызовите `microsoftTeams.settings.setSettings()` во время начальной настройки следующие параметры:

- `entityId` — это пользовательский ИД, который понимается службой и представляет настроенные пользователем данные.
- `configName` — это удобное имя, которое может получить код конфигурации
- `contentUrl` это настраиваемый URL-адрес, который загружается при редактировании пользователем существующей конфигурации соединителя. Этот URL-адрес можно использовать, чтобы упростить обработку дела редактирования в коде.

Как правило, этот вызов является частью обработки события сохранения. Затем при загрузке выше код должен вызвать предварительное переполнение любых параметров или форм в пользовательском интерфейсе `contentUrl` `getSettings()` конфигурации.

#### <a name="handling-removals"></a>Обработка удалений

При желании обработчик событий можно выполнить, когда пользователь удаляет существующую конфигурацию соединителю. Этот обработок регистрируется путем `microsoftTeams.settings.registerOnRemoveHandler()` вызова. Этот обработок можно использовать для выполнения операций очистки, таких как удаление записей из базы данных.

### <a name="including-the-connector-in-your-manifest"></a>Включите соединители в манифест

Вы можете скачать автоматически созданный манифест приложения Teams с портала. Однако прежде чем использовать его для тестирования или публикации приложения, необходимо сделать следующее:

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

Теперь можно запустить среду настройки. Следует помнить, что этот поток полностью проходит в Microsoft Teams в качестве ведущего.

Чтобы убедиться, что действие работает правильно, отправьте `HttpPOST` сообщения [соединителю.](~/webhooks-and-connectors/how-to/connectors-using.md)

## <a name="publish-connectors-for-your-organization"></a>Публикация соединители для организации

Иногда может не потребоваться публиковать приложение соединители в общедоступных AppSource или Store, но вы хотите, чтобы оно было доступно только пользователям в вашей организации. В таких случаях вы можете отправить приложение настраиваемого соединитела в каталог [приложений вашей организации.](~/concepts/deploy-and-publish/apps-publish.md) Таким образом, приложение соединители будет доступно только для этой организации, и вам не потребуется публиковать соединители в общедоступных магазинах.

После отправки пакета приложения для настройки и использования соединители в команде его можно установить из каталога приложений организации, вы предприняв указанные ниже действия.

1. Выберите значок приложений на левой вертикальной панели навигации.
1. В **окне "Приложения"** выберите **соединители.**
1. Выберите соединитель, который нужно добавить, и отобразит всплывающее диалоговое окно.
1. Выберите **"Добавить на панели группы".**
1. В следующем диалоговом окне введите имя команды или канала.
1. Выберите **строку соединители** в правом нижнем углу диалогового окна.
1. Соединители будут доступны в разделе &#9679;&#9679;&#9679; => Дополнительные параметры Соединители Все соединители для команды  =>    =>    =>   для этой команды. Вы можете перейти к этому разделу или найти приложение соединители.
1. Чтобы настроить или изменить соединители, выберите **"Настроить** планку".
